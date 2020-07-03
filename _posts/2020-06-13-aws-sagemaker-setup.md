---
layout: post
title: "Training ML models in the cloud with AWS Sagemaker"
date: 2020-06-13
comments: true
categories:
 - ml
 - sagemaker
 - aws
---

<link rel="canonical" href="https://fairtiq.com/en-ch/tech/training-ml-models-in-the-cloud-with-aws-sagemaker"/>

At some point, when a startup outgrows its first office (which also happens to be the apartment of one of the founders),
it becomes challenging to continue training Machine Learning (ML) models on your laptop, because:

* Training becomes slow as the dataset grows. Also, you cannot close the laptop while training.
* As ML team grows, people need a shared view on model’s performance. 

What’s the next step? Typically it’s a cloud-based platform.
The largest players here are [AWS Sagemaker](https://aws.amazon.com/sagemaker/), [Azure ML](https://azure.microsoft.com/en-in/services/machine-learning/) and [Google AI Platform](https://cloud.google.com/ai-platform).
Those systems are being very actively developed, driven by the high demand.
As a result, they have exploded in the number of features and configurations for various use cases.
The amount of features grows faster than the documentation that is constantly getting outdated.
On top of that, the documentation is often fragmented. You have to check multiple tutorials,all of which use slightly (or not) different examples.
Lastly, tutorials typically walk you through a complete, but toy example (usually with CIFAR data) that is not relevant for a real-life system.

Below, I’ve put together a reference guide for setting up an ML training pipeline with AWS Sagemaker.
It is especially useful when **you want to migrate an existing local ML pipeline**.

I chose Sagemaker for a couple of reasons:

* We already use other AWS services such as S3 and IAM. This way we use a familiar platform and simplify legal aspects for data storage and processing.
* Sagemaker allows to setup an ML training pipeline with few changes to the existing code.

**This guide covers the following topics**:

* Running Sagemaker training jobs with Tensorflow in Docker images. Loading training data from S3.
* Dependency management. Real-life software usually has dependencies on external libraries. This aspect is largely overlooked in tutorials from vendors.
* Circle-CI integration configuration.

Below you can see the overall pipeline architecture that we are going to implement:

<img alt="Sagemaker workflow" src="/images/blog/2020-06-13-aws-sagemaker-setup/Sagemamer workflow.jpg" />

**What’s not (yet) covered**:

* Monitoring and debugging. I will cover this in my next post.
* Hyperparameter tuning / Sagemaker experiments. Here is a video that to learn more about these topics: https://www.youtube.com/watch?v=Tnv6HsT1r4I 
* Distributed training
* Model serving from AWS
* Managing training data through Sagemaker

## Prerequisites

* **Python 3**. AWS Sagemaker starting v1.56.2 supports python 3.7.
* **Tensorflow ≥ 2.1**.
* Python dependencies are pip-installable (either from pypi or github repositories).
* Training/validation/… datasets are stored on S3.

### AWS Resources
When creating S3 buckets, make sure they are all created in the same AWS region, and use the same region when submitting Sagemaker jobs.
Locally you can configure the AWS default region with ``aws configure`` command.

## Packaging your training pipeline

Sagemaker offers two ways to spawn training jobs: using a pre-built image or shipping your own Docker image. We are going for the latter for the following reasons:

* Not being dependent on the supported library versions for pre-built images. Pre-built Sagemaker images typically lag behind the latest library versions. With Docker you can ship any version you want, for example Tensorflow latest dev build.
* Building a custom Docker image allows to include both public and private dependencies in an easy way.

This guide assumes the following directory structure of your ML project:

{% highlight plaintext %}
MY_ML_PROJECT/
  MY_ML_PACKAGE/
    __init__.py
    ...
    train.py
  sagemaker/
    prepare.sh
    build_and_push_image.sh
    Dockerfile
    entrypoint_train.py
    run_sagemaker.py
    requirements.txt
  ....
{% endhighlight %}

Below is the description of the purpose of each file that we’ll need:

* ``prepare.sh``: shell script to prepare the build environment – download private dependencies.
* ``build_and_push_image.sh``: shell script to build a docker image and store it on AWS. Can be called locally or from a CI service. Not needed if you use Circle-CI (see Building an image from Circle-CI below).
* ``Dockerfile``: standard file for Docker that defines how to assemble an image and run our code.
* ``entrypoint_train.py``: This is the entry script that is called by Sagemaker in the Docker container. It reads arguments passed to Sagemaker and handles any errors.
* ``train.py``: python script that loads the data and trains the model. Called by ``entrypoint_train.py``. 
* ``run_sagemaker.py``: Python script to start the training on AWS Sagemaker. Can be called locally or from a CI service.
* ``requirements.txt``: requirements file for packages needed specifically for training.

Let’s now look at the files and their purpose in detail.
The repository with all the files from this guide is also available at: https://github.com/fairtiq/sagemaker-templates/tree/master/sagemaker-docker-basic.

### Building a docker image

First, ``prepare.sh`` script prepares the environment – makes sure our entry point is executable and downloads private dependencies:

{% highlight shell %}
#!/usr/bin/env bash

# Fail on errors
set -o errexit

__dir="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"

chmod +x ${__dir}/entrypoint_train.py

rm -rf tmp
# PRIVATE DEPENDENCIES
echo "Cloning PRIVATE-REPO..."
git clone git@github.com:COMPANY/PRIVATE-REPO.git tmp/PRIVATE-REPO
{% endhighlight %}

Next is the script ``build_and_push_image.sh`` to build a docker image and push it to AWS. You need to customize/setup the following variables:

* ``REPO_NAME`` - the name of the repository to create/add on ECR (Elastic Container Registry). It’s an AWS service that stores your docker images.
* Replace ``git@github.com:COMPANY/PRIVATE-REPO.git`` with the address of the repository containing your private dependency. Add more if needed.
* Make sure to run ``aws configure`` to setup the AWS region you are working from. **The region has to match the S3 bucket region when your training/validation data is stored**.

Change the image tag if needed. The script uses ``latest`` tag (line 18).

{% highlight shell %}
#!/usr/bin/env bash

# Fail on errors
set -o errexit

# call prepare.sh in the same directory
__dir="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
sh ${__dir}/prepare.sh

# The name of the image in the AWS registry
repo_name=REPO_NAME

account=$(aws sts get-caller-identity --query Account --output text)

# Get the region defined in the current configuration
region=$(aws configure get region)

fullname="${account}.dkr.ecr.${region}.amazonaws.com/${repo_name}:latest"

# If the repository doesn't exist in ECR, create it.

aws ecr describe-repositories --repository-names "${repo_name}" > /dev/null 2>&1

if [ $? -ne 0 ]
then
    aws ecr create-repository --repository-name "${repo_name}" > /dev/null
fi

# Get the login command from ECR and login
aws ecr get-login-password --region ${region} | docker login --username AWS --password-stdin ${account}.dkr.ecr.${region}.amazonaws.com

# Build the docker image locally with the image name and then push it to ECR
# with the full name.

docker build  -t ${repo_name} -f ${__dir}/Dockerfile .
docker tag ${repo_name} ${fullname}

docker push ${fullname}
{% endhighlight %}

*Originally published at [fairtiq.com](https://fairtiq.com/en-ch/tech/training-ml-models-in-the-cloud-with-aws-sagemaker)*