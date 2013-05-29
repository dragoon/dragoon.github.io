---
layout: post
title: "Migrating bitbucket.org issues between the repos"
date: 2012-12-16
comments: false
categories:
 - en
 - bitbucket
 - python
---


Bitbucket is definetly a nice code hosting system, which offers you private repositories for free. This feature favourably distinguishes it from <a href="http://github.com/">GitHub</a>, for example.

Until October 2011, bitbucket only supported <i>Mercurial</i> ****as a DVCS system to store your repositories, but then <i>Git </i>support was introduced as well. Unfortunately, it was not possible to convert your project to Git by simply clicking on a button. You have to move everything **to a new repository** yourself using <i>hg-fast-export</i> or something.

But let's say you want to also move all your issues to a new repo. It is not possible either. There still exists an open ticket created 3 years ago regarding this problem: <a href="https://bitbucket.org/site/master/issue/1642/allow-moving-tickets-over-to-another">https://bitbucket.org/site/master/issue/1642/allow-moving-tickets-over-to-another</a>. So, since I did not found any reasonable solution (except this <a href="http://mgaitan.github.com/posts/migrando-issues-entre-proyectos-de-bitbucket.html">post on Spanish</a> from the comments of the ticket), I deciced to create this simple gist to solve the problem: <a href="https://gist.github.com/4297504">https://gist.github.com/4297504</a>.

Basically, it uses the <a href="https://confluence.atlassian.com/display/BITBUCKET/Using+the+Bitbucket+REST+APIs">bitbucket API</a> through the Basic Auth to access the data and clones the following fields to the target repository: **title, content (description), priority, status, kind (bug/enhancement/etc.)**
**
**Happy migrating!
