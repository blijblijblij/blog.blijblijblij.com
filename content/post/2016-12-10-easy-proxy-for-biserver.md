+++
draft = false
title = "Setup an easy reverse proxy to the biserver"
date = "2016-12-10T13:00:00+01:00"
author = "Rogier Wessel"
comments = true
share = true
image = "images/cover.jpg"
slug = "easy-proxy-for-biserver"
tags = ["docker", "pentaho", "proxy"]
post = "/:year/:month/:day/:slug.html"

+++

# Problem

You have a biserver serving up information either directly or embedded into
some website. You need to open up the biserver to the rest of the world but want
to prevent access to certain endpoints. These endpoints might serve only internal
consumers, or have security implications.

We need to limit the attack service of a biserver!

![proxy it](/images/mayday.png "proxy it")

Traditionally one would spin up a new server, add an apache config to proxy forward
some requests to the backend. This adds complexity, moving parts, and lowers
agility.

In this post I'll suggest a simplification of the same approach, just in a
slightly more flexible way, obviously we'll containerize it.

# Solution

## Ingredients

- a [haproxy container](https://github.com/docker/dockercloud-haproxy) with a pretty impressive featureset
- a biserver 6.1 container with a wildly impressive `HelloWorld` cde dashboard `/pentaho/api/repos/%3Apublic%3AHelloWorld.wcdf/generatedContent`
- a canary container that will informs us about missing resources
- a docker-composition to glue these together:

```shell
version: '2'
services:
  biserver:
    image: pentaho/biserver:6.1
    ports:
      - 8080:8080
    environment:
      - VIRTUAL_HOST=...
      - VIRTUAL_HOST_WEIGHT=2
  canary:
    image: httpd:latest
    environment:
      - VIRTUAL_HOST=http://*
      - VIRTUAL_HOST_WEIGHT=1
  proxy:
    image: dockercloud/haproxy
    links:
      - biserver
      - canary
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    ports:
      - 80:80
```

## Round 1

We utilise the `VIRTUAL_HOST` [options](https://github.com/docker/dockercloud-haproxy#global-and-default-settings-of-haproxy) of the proxy to whitelist our epic HelloWorld dashboard. By giving the proxy a higher `VIRTUAL_HOST_WEIGHT` we force traffic to first route via this `VIRTUAL_HOST` everything else falls through onto the canary container.

```shell
VIRTUAL_HOST=http://*/pentaho/api/repos/%3Apublic%3AHelloWorld.wcdf/generatedContent
```

Looking at the dashboard directly.

![unproxied](/images/2016-12-10_biserver direct.png "unproxied")

Now, lets view it via the proxy
![proxied](/images/2016-12-10_biserverproxied.png "proxied")

But oh, the horror of my carefully crafted indenting, it has gone all haywire. And when we inspect the page we see what's going wrong:

![styling horrors](/images/2016-12-10_styling_horrors.png "styling horrors")

And funny enough, now the `canary` container comes to offer the same insight as well:

```shell
canary_1    | 172.18.0.4 - - [10/Dec/2016:20:09:49 +0000] "GET /pentaho/api/repos/pentaho-cdf/js/cdf-bootstrap-script-includes.js?v=decdbcb3b01341682f2ef9799798313c HTTP/1.1" 404 263
canary_1    | 172.18.0.4 - - [10/Dec/2016:20:09:49 +0000] "GET /pentaho/api/repos/pentaho-cdf/css/cdf-bootstrap-style-includes.css?v=7bc42bb099ded22348e9c9b992045d67 HTTP/1.1" 404 264
canary_1    | 172.18.0.4 - - [10/Dec/2016:20:09:49 +0000] "GET /pentaho/api/repos/pentaho-cdf-dd/js/CDF.js?v=7591bba3804971aeae31ca943022aba2 HTTP/1.1" 404 240
canary_1    | 172.18.0.4 - - [10/Dec/2016:20:09:49 +0000] "GET /pentaho/api/repos/pentaho-cdf-dd/css/CDF-CSS.css?v=9dd48fd0265f0d8bcc30ac6afec3f0ff HTTP/1.1" 404 246
canary_1    | 172.18.0.4 - - [10/Dec/2016:20:09:52 +0000] "GET /pentaho/api/repos/pentaho-cdf/js/cdf-bootstrap-script-includes.js?v=decdbcb3b01341682f2ef9799798313c HTTP/1.1" 404 263
canary_1    | 172.18.0.4 - - [10/Dec/2016:20:09:52 +0000] "GET /pentaho/api/repos/pentaho-cdf/css/cdf-bootstrap-style-includes.css?v=7bc42bb099ded22348e9c9b992045d67 HTTP/1.1" 404 264
canary_1    | 172.18.0.4 - - [10/Dec/2016:20:09:52 +0000] "GET /pentaho/api/repos/pentaho-cdf-dd/js/CDF.js?v=7591bba3804971aeae31ca943022aba2 HTTP/1.1" 404 240
canary_1    | 172.18.0.4 - - [10/Dec/2016:20:09:52 +0000] "GET /pentaho/api/repos/pentaho-cdf-dd/css/CDF-CSS.css?v=9dd48fd0265f0d8bcc30ac6afec3f0ff HTTP/1.1" 404 246
canary_1    | 172.18.0.4 - - [10/Dec/2016:20:11:09 +0000] "GET /pentaho/api/repos/pentaho-cdf/js/cdf-bootstrap-script-includes.js?v=decdbcb3b01341682f2ef9799798313c HTTP/1.1" 404 263
canary_1    | 172.18.0.4 - - [10/Dec/2016:20:11:09 +0000] "GET /pentaho/api/repos/pentaho-cdf/css/cdf-bootstrap-style-includes.css?v=7bc42bb099ded22348e9c9b992045d67 HTTP/1.1" 404 264
canary_1    | 172.18.0.4 - - [10/Dec/2016:20:11:09 +0000] "GET /pentaho/api/repos/pentaho-cdf-dd/js/CDF.js?v=7591bba3804971aeae31ca943022aba2 HTTP/1.1" 404 240
```
## Round 2
So we whitelist two more paths:

- `/pentaho/api/repos/pentaho-cdf/js/*`
- `/pentaho/api/repos/pentaho-cdf/css/*`

```shell
VIRTUAL_HOST=http://*/pentaho/api/repos/%3Apublic%3AHelloWorld.wcdf/generatedContent,http://*/pentaho/api/repos/pentaho-cdf/css/*,http://*/pentaho/api/repos/pentaho-cdf/js/*
```

Et voila, indenting back from the death, but carefully proxied for only that particular resource we wanted to expose to the world `:-)`
![epic](/images/2016-12-10_epic_dashboard.png "epic")

So the final composition looks like:


```shell
version: '2'
services:
  biserver:
    image: pentaho/biserver:6.1
    ports:
      - 8080
    environment:
      - VIRTUAL_HOST=http://*/pentaho/api/repos/%3Apublic%3AHelloWorld.wcdf/generatedContent,http://*/pentaho/api/repos/pentaho-cdf/css/*,http://*/pentaho/api/repos/pentaho-cdf/js/*
      - VIRTUAL_HOST_WEIGHT=2
      - GZIP_COMPRESSION_TYPE=text/html text/plain text/css text/javascript application/json
  canary:
    image: httpd:latest
    environment:
      - VIRTUAL_HOST=http://*
      - VIRTUAL_HOST_WEIGHT=1
      - GZIP_COMPRESSION_TYPE=text/html text/plain text/css text/javascript application/json
  proxy:
    image: dockercloud/haproxy
    links:
      - biserver
      - canary
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    ports:
      - 80:80
```

We have locked up the biserver completely, and we can dive deeper into the [magic of the haproxy container](https://github.com/docker/dockercloud-haproxy#global-and-default-settings-of-haproxy),
as it can do easy ssl termination as well, just change the proxy to:

```shell
proxy:
  image: dockercloud/haproxy
  environment:
    - DEFAULT_SSL_CERT=-----> my cert goes here
  links:
    - biserver
    - canary
  volumes:
    - /var/run/docker.sock:/var/run/docker.sock
  ports:
    - 443:443
```
