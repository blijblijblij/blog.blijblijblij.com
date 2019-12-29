+++
date = "2016-05-11T07:00:32+02:00"
draft = false
author = "Rogier Wessel"
comments = true
image = "images/cover.jpg"
menu = ""
share = true
slug = "pentahanl-spring-meetup"
tags = ["meetup", "pentaho"]
title = "Pentaho NL spring meetup"
post = "/:year/:month/:day/:slug.html"

+++
Last month we gathered for the second Pentaho NL meetup. [@Incentro](https://www.twitter.com/incentro) were sponsoring the location (their office at former Airport Ypenburg) as well as some excellent food and drinks, much appreciated guys!

Again we had an impressive turn up, some new faces, some more familiar, a good mix for sharing and discussing life, the universe, and well, [Pentaho](https://www.twitter.com/pentaho) stuff...

# Data Virtualization with PDI Community Edition
*Edwin Weber*

![alt text](https://raw.githubusercontent.com/blijblijblij/blog.blijblijblij.com/c38182b984a7481a01c0b0e84eb3b2e4a926eff7/images/2016-04-19-edwin.jpg "Edwin on fire!")

Edwin challenged the demo-gods, they got the better off him. But Edwin is a master (karate wise, as well as pentaho wise). He reclaimed his mastery and demo-ed Data Virtualization using the thin jdbc driver running sql queries on top of data transformations. Apparently this functionality still needs some hammering to get it to work. But from what I have heared Edwins work has already been relayed to another master, a new [Diethard Steiner](https://twitter.com/diethardsteiner) post should be in the makings.

As for [Edwins](https://twitter.com/edwin_weber) talk, here is the [transscript](https://github.com/blijblijblij/blog.blijblijblij.com/raw/0edeaeef6e7778ebac04579505e3418470d3eb91/pdf/20160503_data_virtualization_demo.pdf).

# Datastax Cassandra plugin
*Rudmer van Dijk*
*The current Cassandra plugin from Pentaho uses an old driver which is unable to support secure SSL connections to the cluster. At Incentro we created a new plugin that utilises the Datastax driver so we can use the secure connection. I'll give a walkthrough and demonstration of the three steps in this plugin.*

Rudmer gave a demo about their newly developed Data Cassandra driver taking us through all functionalities.

![alt text](https://raw.githubusercontent.com/blijblijblij/blog.blijblijblij.com/master/images/2016-04-13-cassandra-driver.png "In the marketplace")

It has been released from the marketplace, hooray on that!

# Tips and Tricks of using JavaScript in PDI
*Julien Hofstede*

*"We all agree: Kettle is awesome. But sometimes seemingly easy things are hard to accomplish, or just not possible with Kettle. I'll show some easy and advanced uses of the JavaScript Step in PDI such as prompts, dynamic accessing of rows, calculations and filtering of rows."*

Julien talk was very interesting, stressing the balance between doing it the Etl / pentaho way versus fixing it in one go in a javascript step. The javascript step is a very powerfull step (dating back to that very beginning of PDI) enabling you to dive deep inside the Pentaho data-integration application and exposing api's unknown to most!

His talk can be found [here](https://github.com/blijblijblij/blog.blijblijblij.com/raw/master/pdf/20160513_JavaScript%20in%20PDI.pdf), but make sure you dive into the [demo samples](https://github.com/blijblijblij/blog.blijblijblij.com/raw/master/pdf/JavaScript%20in%20PDI.zip) as well!!!

To conclude, another inspriring Pentaho NL meetup!
