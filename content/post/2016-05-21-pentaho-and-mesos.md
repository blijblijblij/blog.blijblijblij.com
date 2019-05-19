+++
date = "2016-05-21T11:06:05+02:00"
title = "Running pentaho on mesos - part 1"
draft = false
author = "Rogier Wessel"
comments = true
image = "images/cover.jpg"
menu = ""
share = true
slug = "pentaho-and-mesos"
tags = ["mesos", "pentaho"]
post = "/:year/:month/:day/:slug.html"
+++

# Introduction
I have been amazed by the ease of getting software through the software development cycle once you start doing it the [Docker](https://www.docker.com/) way. I picked it up soon after [it came to light](http://www.wired.com/2013/09/docker/), and hammered it hard. At that point I got all developers aligned to use Docker as well.

As we started using Docker more extensively, combining different Frontends services and Backends services through Docker compositions, running multiple hosts, intranet, things started to get a bit more complicated.

[Adrian Mouat](https://twitter.com/adrianmouat) acknowledged my next step in a piece he wrote for Oreilly [Swarm v. Fleet v. Kubernetes v. Mesos Comparing different orchestration tools](https://www.oreilly.com/ideas/swarm-v-fleet-v-kubernetes-v-mesos) my prefered orchestration framework for our containers would be Mesos.

# Define
This is an overview of a mesos cluster in its simplest form.
![Mesos architectural overview](https://raw.githubusercontent.com/blijblijblij/blog.blijblijblij.com-hugo/9dafdf22f19d04c63eb47e2c9681884694887156/static/images/mesos-arch.png)
[Source](https://www.oreilly.com/ideas/swarm-v-fleet-v-kubernetes-v-mesos)

- **The mesos-master** is the central part of the cluster, it controls all jobs on the cluster. Usually multiple masters are running on a cluster, thereby given it HA capabilities, especially when running the masters in different [availability zones](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html#concepts-regions-availability-zones).
- **The marathon scheduler** is the scheduler for long running processes, a webserver, a carte server, a baserver, ... The functionality of Marathon on the cluster is often compared to what `init.d` leverages on a linux system. To run services, keep them running, scale them etc.
- **The chronos scheduler** is a scheduler batch task, and as such often compared to `cron`
- **The mesos slaves aka agents** run the actual jobs as directed by the mesos master(s)
- **Zookeeper** is used for master elections, coordination and to persist configuration throughout the cluster.

There is so much more to be told about mesos, but I suggest you just `Run, Forrest, Run!` to [Oreilly](http://ssearch.oreilly.com/?q=mesos&x=0&y=0), [Manning](https://www.manning.com/books/mesos-in-action) or some other it-drug delivery service and read up on this topic.
# Create
I am going to assume a working [docker](https://docs.docker.com/engine/installation/) / [docker-compose](https://docs.docker.com/compose/install/) / [docker-machine](https://docs.docker.com/machine/install-machine/) setup, some recent hardware.

For now I will focus on a virtualbox based cluster running locally. I have created a crude but usefull bash-script to get you up and running, it cleans, creates masters, slave and a loadbalancer by utilising docker-machine. I have 4cpu, 16G of RAM at my disposal, just tinker with `virtualbox-cpu-count`, `virtualbox-memory` and `virtualbox-disk-size` to make this baby fit your needs.

```
#!/bin/sh
clear

echo "creating my epic local cluster"

clean() {
  echo "---> rm old machines, no mercy baby!"
  docker-machine rm -f mesos-lb1 mesos-m1 mesos-m2 mesos-m3 mesos-s1 mesos-s2 > /dev/null
}

create_masters() {
  echo "---> create masters"
  echo "---> create mesos-m1"
  docker-machine create -d virtualbox \
    --virtualbox-cpu-count "1" \
    --virtualbox-memory "1024" \
    --virtualbox-disk-size "50000" \
    mesos-m1

  echo "---> create mesos-m2"
  docker-machine create -d virtualbox \
    --virtualbox-cpu-count "1" \
    --virtualbox-memory "1024" \
    --virtualbox-disk-size "50000" \
    mesos-m2

  echo "---> create mesos-m3"
  docker-machine create -d virtualbox \
    --virtualbox-cpu-count "1" \
    --virtualbox-memory "1024" \
    --virtualbox-disk-size "50000" \
    mesos-m3
}

create_slaves() {
  echo "---> create slaves"
  echo "---> create mesos-s1"
  docker-machine create -d virtualbox \
    --virtualbox-cpu-count "2" \
    --virtualbox-memory "4092" \
    --virtualbox-disk-size "50000" \
    mesos-s1

  echo "---> create mesos-s2"
  docker-machine create -d virtualbox \
      --virtualbox-cpu-count "2" \
      --virtualbox-memory "4092" \
      --virtualbox-disk-size "50000" \
      mesos-s2
}

create_loadbalancer() {
  echo "---> create loadbalancer"
  echo "---> create mesos-lb1"
  docker-machine create -d virtualbox \
    --virtualbox-cpu-count "1" \
    --virtualbox-memory "1024" \
    --virtualbox-disk-size "50000" \
    mesos-lb1
}
main() {
  clean
  create_masters
  create_slaves
  create_loadbalancer
  echo "done"
}

main

```

After running this script, check the results:

```
docker-machine ls | grep virtualbox
mesos-lb1                    -        virtualbox   Running   tcp://192.168.99.105:2376           v1.11.1   
mesos-m1                     -        virtualbox   Running   tcp://192.168.99.100:2376           v1.11.1   
mesos-m2                     -        virtualbox   Running   tcp://192.168.99.101:2376           v1.11.1   
mesos-m3                     -        virtualbox   Running   tcp://192.168.99.102:2376           v1.11.1   
mesos-s1                     -        virtualbox   Running   tcp://192.168.99.103:2376           v1.11.1   
mesos-s2                     -        virtualbox   Running   tcp://192.168.99.104:2376           v1.11.1
```

That was easy!

# Run
