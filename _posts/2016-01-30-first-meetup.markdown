---
layout:     post
title:      "First pentaho nl meetup!"
subtitle:   "beer, pizza, a lot of people!"
date:       2016-01-30 12:00:00
author:     "Rogier Wessel"
header-img: "img/post-bg-05.jpg"
---

<p>Busy times, so with a slight delay a recap of our very first <a href="http://www.meetup.com/Pentaho-NL-Meetup/">pentaho NL meetup</a>.
</p>
<p>ReelMetrics supplied a nice venue for this first meetup, took care off
much appreciated beers and pizza's. After these refreshments we had some nice talks
covering a wide range of functionalities within the Pentaho ecosphere.</p>

# Intro
<p>From a yearly gathering somewhere in Europe, why not do a dutch equivalent every
couple of months?! As open-source is thriving, community initiatives become even
more important, and more than enough people doing Pentaho stuff in The Netherlands,
so we gave it a try!</p>

<p>Some general "goals" to our meetup:</p>

- to have FUN!
- to learn!
- to share!
- for noobs, super-dupper-master-hackers and everything in between!
- every couple of months-ish

**Note**, if a traveling pentaho rockstars comes along, we should do a adhoc meetup
and seize that opportunity!

# Pentaho and Docker Docker Docker!
*Rogier Wessel* Ok, I must admit, I am a big fan of both Pentaho and Docker. During this talk I explained
first the basic building blocks that make up docker. Then talked about glueing
services together into a docker composition. Finally once you start growing that
infrastructure other problems arise, orchestration of docker instances running
on multiple hosts gets complicated, and running a couple compositions doesn't cut
it anymore.

<p>I gathered a lot of direction on orchestration based on the sound analyses
by <a href="https://twitter.com/adrianmouat">Adrian Mouat's</a> article on O'reilly radar <a href="http://radar.oreilly.com/2015/10/swarm-v-fleet-v-kubernetes-v-mesos.html">Swarm v. Fleet v. Kubernetes v. Mesos</a>.</p>

<p>Based on that article I continued my quest in orchestration and investigated <a href="http://mesos.apache.org/">Apache mesos</a>
extensively. The second half of my talk was demo time. When you do Docker with Pentaho software
on Apache mesos, what are the components that make up the infrastructure, how is
everything interconnected, and why does this complicated infrastructure make sense
once your infrastructure grows beyond a certain size.</p>

<iframe src="https://docs.google.com/presentation/d/1qcNw-m7f7XHjGA6KfEjd3mqR03gsqM2N6kNDCTgP5pA/embed?start=false&loop=false&delayms=3000" frameborder="0" width="700" height="422" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

<p>All code about creating and running a Mesos cluster is on my github page
https://github.com/blijblijblij/docker-mesos: </p>

- <a href="https://github.com/blijblijblij/docker-mesos/blob/develop/create/create-virtualbox-cluster.sh">building a local virtualbox cluster</a>
- <a href="https://github.com/blijblijblij/docker-mesos/blob/develop/create/create-generic-ssh-cluster.sh">building a cluster via ssh</a>
- <a href="https://github.com/blijblijblij/docker-mesos/blob/develop/create/create-aws-cluster.sh">or directly via the aws api</a>
- <a href="https://github.com/blijblijblij/docker-mesos/tree/develop/run">and running that cluster</a>

#CTools Dashboards are Awesome!
*Julien Hofstede* This presentation showed some techniques to make development of the dashboards easier like reusable components and global settings. And even to create your own component! Take the step beyond CDE and leverage the full power of CDF! No knowledge or experience with CDF? No worries! It will for sure help you to understand the concept of CDF better.

Julien also demo-ed a lot, styling a set of components in an instant just by implementing a standard layout, and reusing that in several graphs extending that standard layout!

#The Community Contributed JDBC Metadata Step for Pentaho Data integration
*Roland Bouman* <a href="https://github.com/rpbouman/pentaho-pdi-plugin-jdbc-metadata">The Community Contributed JDBC Metadata Step for Pentaho Data integration</a> enables you to use database metadata to drive transformations. You can use it to track database schema changes, to generate DDL, and even to implement datawarehouse automation. His presentation demonstrated the features of the plugin and illustrated how you can use it in your kettle transformations.

<p>Roland never seems to stop coming up with new functionalities giving new insights, his code is all up on <a href="https://github.com/rpbouman">github</a>. He could do with some extra eyes on the code, or some extra code to further extent his current work. So feel free to join and <a href="https://twitter.com/rolandbouman">give him a nudge</a>!</p>

#What's up next?!
<p>Well, a lot of people turned up, some even took a hotel because of their long travels, big up for that!</p>

<p>Next to ReelMetrics some other sponsors came forward, for a location, pitch in for some beers :-). Also several people already offered to give a talk about some subject. <a href="https://twitter.com/dennisintgroen">Dennis</a> wouldn't mind diving into CDE widgets, and offering another view to reusable components along the lines of Juliens talk. <a href="https://twitter.com/edwin_weber">Edwin</a> had something up his sleeve. Even <a href="https://twitter.com/codek1">Dan Keeley</a> offered to come over and give a talk, we would love to accept his offer, and learn from his extensive experience.</p>

<p>So, enough momentum, looking forward to our next meetup!!!</p>
