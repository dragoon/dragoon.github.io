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


Bitbucket is definetly a nice code hosting system, which offers you private repositories for free. This feature favourably distinguishes it from <a href="http://github.com/">GitHub</a>, for example.<br /><br />Until October 2011, bitbucket only supported&nbsp;<i>Mercurial</i><b> </b>as a DVCS system to store your repositories, but then <i>Git </i>support was introduced as well. Unfortunately, it was not possible to convert your project to Git by simply clicking on a button. You have to move everything <b>to a new repository</b> yourself using <i>hg-fast-export</i> or something.<br /><br />But let's say you want to also move all your issues to a new repo. It is not possible either.&nbsp;There still exists an open ticket created 3 years ago regarding this problem:&nbsp;<a href="https://bitbucket.org/site/master/issue/1642/allow-moving-tickets-over-to-another">https://bitbucket.org/site/master/issue/1642/allow-moving-tickets-over-to-another</a>.&nbsp;So, since I did not found any reasonable solution (except this <a href="http://mgaitan.github.com/posts/migrando-issues-entre-proyectos-de-bitbucket.html">post on Spanish</a>&nbsp;from&nbsp;the comments of the ticket),&nbsp;I deciced to create this simple gist to solve the problem:&nbsp;<a href="https://gist.github.com/4297504">https://gist.github.com/4297504</a>.<br /><br />Basically, it uses the <a href="https://confluence.atlassian.com/display/BITBUCKET/Using+the+Bitbucket+REST+APIs">bitbucket API</a>&nbsp;through the Basic Auth&nbsp;to access the data and clones the following fields to the target repository:<b> title, content (description), priority, status, kind (bug/enhancement/etc.)</b><br /><b><br /></b>Happy migrating!</div>
