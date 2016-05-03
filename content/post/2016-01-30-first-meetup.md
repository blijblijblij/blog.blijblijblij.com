+++
author = "Rogier Wessel"
comments = true
date = "2016-01-30T23:02:54+02:00"
draft = false
image = "images/cover.jpg"
menu = ""
share = true
slug = "2016-01-30-first-meetup"
tags = ["pentaho", "meetup"]
title = "First pentaho nl meetup!"

+++

Busy times, so with a slight delay a recap of our very first [pentaho NL meetup](http://www.meetup.com/Pentaho-NL-Meetup/).

ReelMetrics supplied a nice venue for this first meetup, took care off much appreciated beers and pizza's. After these refreshments we had some nice talks covering a wide range of functionalities within the Pentaho ecosphere.

# Intro
From a yearly gathering somewhere in Europe, why not do a dutch equivalent every couple of months?! As open-source is thriving, community initiatives become even more important, and more than enough people doing Pentaho stuff in The Netherlands, so we gave it a try!

Some general "goals" to our meetup:

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

I gathered a lot of direction on orchestration based on the sound analyses by [Adrian Mouat's](https://twitter.com/adrianmouat) article on O'reilly radar [Swarm v. Fleet v. Kubernetes v. Mesos](http://radar.oreilly.com/2015/10/swarm-v-fleet-v-kubernetes-v-mesos.html).

Based on that article I continued my quest in orchestration and investigated [Apache Mesos](http://mesos.apache.org/)
extensively. The second half of my talk was demo time. When you do Docker with Pentaho software on Apache mesos, what are the components that make up the infrastructure, how is everything interconnected, and why does this complicated infrastructure make sense once your infrastructure grows beyond a certain size.

<iframe src="https://docs.google.com/presentation/d/1qcNw-m7f7XHjGA6KfEjd3mqR03gsqM2N6kNDCTgP5pA/embed?start=false&loop=false&delayms=3000" frameborder="0" width="700" height="422" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

All code about creating and running a Mesos cluster is on [my github page](https://github.com/blijblijblij/docker-mesos):

- [building a local virtualbox cluster](https://github.com/blijblijblij/docker-mesos/blob/develop/create/create-virtualbox-cluster.sh)
- [building a cluster via ssh](https://github.com/blijblijblij/docker-mesos/blob/develop/create/create-generic-ssh-cluster.sh)
- [or directly via the aws api](https://github.com/blijblijblij/docker-mesos/blob/develop/create/create-aws-cluster.sh)
- [and running that cluster](https://github.com/blijblijblij/docker-mesos/tree/develop/run)

# CTools Dashboards are Awesome!
*Julien Hofstede* This presentation showed some techniques to make development of the dashboards easier like reusable components and global settings. And even to create your own component! Take the step beyond CDE and leverage the full power of CDF! No knowledge or experience with CDF? No worries! It will for sure help you to understand the concept of CDF better.

Julien also demo-ed a lot, styling a set of components in an instant just by implementing a standard layout, and reusing that in several graphs extending that standard layout!

# The Community Contributed JDBC Metadata Step for Pentaho Data integration
*Roland Bouman* [The Community Contributed JDBC Metadata Step for Pentaho Data integration](https://github.com/rpbouman/pentaho-pdi-plugin-jdbc-metadata) enables you to use database metadata to drive transformations. You can use it to track database schema changes, to generate DDL, and even to implement datawarehouse automation. His presentation demonstrated the features of the plugin and illustrated how you can use it in your kettle transformations.

Roland never seems to stop coming up with new functionalities giving new insights, his code is all up on [github](https://github.com/rpbouman). He could do with some extra eyes on the code, or some extra code to further extent his current work. So feel free to join and [give him a nudge](https://twitter.com/rolandbouman)!

# What's up next?!
Well, a lot of people turned up, some even took a hotel because of their long travels, big up for that!

Next to ReelMetrics some other sponsors came forward, for a location, pitch in for some beers :-). Also several people already offered to give a talk about some subject. [Dennis](https://twitter.com/dennisintgroen) wouldn't mind diving into CDE widgets, and offering another view to reusable components along the lines of Juliens talk. [Edwin](https://twitter.com/edwin_weber) had something up his sleeve. Even [Dan Keeley]https://twitter.com/codek1 offered to come over and give a talk, we would love to accept his offer, and learn from his extensive experience.

So, enough momentum, looking forward to our next meetup!!!
