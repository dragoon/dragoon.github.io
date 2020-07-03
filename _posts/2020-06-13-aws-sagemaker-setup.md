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

<img alt="Sagemaker workflow" src="/images/blog/2020-06-13-aws-sagemaker-setup/Sagemaker workflow.jpg" />

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
The repository with all the files from this guide is also available at:
<https://github.com/fairtiq/sagemaker-templates/tree/master/sagemaker-docker-basic>.

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

Whenever you push an image to the ECR with the same tag, the previous image will become untagged, but remain in the repository.
If you want to clean untagged images automatically, you can set up a lifecycle policy as described here:
<https://aws.amazon.com/blogs/compute/clean-up-your-container-images-with-amazon-ecr-lifecycle-policies/>

### Building an image on Circle-CI

[Circle-CI](https://circleci.com/) is a Continuous Integration cloud service.
As we use it at FAIRTIQ, I have created a job to build and push image to ECR with it.
Circle-CI provides a convenient [aws-ecr orb](https://circleci.com/orbs/registry/orb/circleci/aws-ecr)
that already has the ``build-and-push-image`` command that we need.

{% highlight yaml %}

orbs:
  aws-ecr: circleci/aws-ecr@6.8.2
...

sagemaker_build:
  docker:
    - image: circleci/python:3.7
  steps:
    - setup_remote_docker:
        docker_layer_caching: true
    - add_ssh_keys # SSH keys for git clone your dependencies
    - checkout
    - run:
        name: Prepare setup
        command: ./sagemaker/prepare.sh
    - aws-ecr/build-and-push-image:
        account-url: AWS_ECR_ACCOUNT_URL
        aws-access-key-id: AWS_ACCESS_KEY_ID
        aws-secret-access-key: AWS_SECRET_ACCESS_KEY
        create-repo: true
        dockerfile: ./sagemaker/Dockerfile
        path: .
        region: AWS_REGION
        repo: REPO_NAME
        tag: $CIRCLE_BRANCH
        
{% endhighlight %}

The config reads the branch name you are working on via the ``$CIRCLE_BRANCH`` variable and uses it as an image tag,
so that you can have separate images for each branch/pull request.

Make sure to provide the following context variables to the job: `AWS_ECR_ACCOUNT_URL`, `AWS_ACCESS_KEY_ID`,
`AWS_SECRET_ACCESS_KEY` and `AWS_REGION`. Then replace the `REPO_NAME` and `MY_ML_PACKAGE` placeholders with your values.

The `AWS_ACCESS_KEY_ID` should belong to a user with permissions to push images to ECR.
I have created a user `circleci-aws-ecr-push` and attached an existing policy called `AmazonEC2ContainerRegistryPowerUser`:

<img alt="aws circle ci push permissions" src="/images/blog/2020-06-13-aws-sagemaker-setup/aws_circleci_user.png" />

### Dockerfile

Both `build_and_push_image.sh` and Circle-CI job call the `docker build` command with a Dockerfile as an argument.
[Dockerfile](https://docs.docker.com/engine/reference/builder/) describes how to build the container and what to package in it.
Below is the file I am using for our ML system with the comments explaining the purpose of operations:

{% highlight Docker %}

FROM tensorflow/tensorflow:2.2.0-gpu

RUN pip install sagemaker-containers

RUN apt-get update && apt-get install -y MY_EXTRA_LIBS

# /opt/ml and all subdirectories are used by SageMaker,
# we use the /opt/ml/code subdirectory to store our ML package code.

# copy the private dependencies that we downloaded with git clone to the container
COPY ./tmp/my-private-package /tmp/my-private-package
# I keep a separate sagemaker sub-package to separate the requirements file 
COPY ./sagemaker/requirements.txt /tmp/requirements.txt

# install private and public dependencies
RUN pip install /tmp/my-private-package -r /tmp/requirements.txt

#` -- /opt/ml/code
#    `-- your-ml-package
#    |-- entrypoint_train.py

COPY ./MY_ML_PACKAGE /opt/ml/code/your-ml-package
# copy the entrypoint file to the code directory
COPY ./sagemaker/entrypoint_train.py /opt/ml/code/entrypoint_train.py
WORKDIR /opt/ml/code

# add working directory to PYTHONPATH to make imports from your ML package
ENV PYTHONPATH="/opt/ml/code:${PYTHONPATH}"

# argument to sagemaker what we want to run
ENV SAGEMAKER_PROGRAM entrypoint_train.py

{% endhighlight %}

The process here is very straightforward. We first install the necessary system libs with apt-get,
copy and install private and public python dependencies, copy your ML package
into `/opt/ml/code` (but it can be anything really), and set the special `SAGEMAKER_PROGRAM` variable for Sagemaker to specify the entrypoint file.

⚠ Tensorflow images on DockerHub use Python 3.6, so if you need 3.7 – you’ll need to build an image from another base.

## Entrypoint

*Originally published at [fairtiq.com](https://fairtiq.com/en-ch/tech/training-ml-models-in-the-cloud-with-aws-sagemaker)*