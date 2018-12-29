A Docker **application container** usually exposes an Internet service to the
world. This page describes some important notes on how to give **Internet
access**.

## Open All Docker IP Addresses

Create the original Docker image **IP address** set to the _meta value_
**0.0.0.0** and the service's
[EXPOSE](https://docs.docker.com/engine/reference/builder/#/expose)d port
number.

  * See [the 0.0.0.0 Wikipedia page](https://en.wikipedia.org/wiki/0.0.0.0)
  * In the context of servers, 0.0.0.0 means **all IPv4 addresses on the local machine**.

## Run Docker with Port Mappings

Create the initial **application container** from the **image** using _port
mappings_. The **image's Dockerfile** must **EXPOSE** ports to the host
machine.

Explicitly Map Port Numbers

Always use the explicit port mapping, **docker run ... -p 8080:80.** Do not
use the _implied mapping_ , **docker run ... -P** which sets the public port
to the **EXPOSE** number. The latter is confusing.

 **Run a New Container from an Image with Port Assignment**

    
    
    # EXPOSE image port 80 to the host as the alternate port 8089.
    $ docker run -d -t <image tag> -p 8089:80

## Find Occupied Ports

Use the simple script below to **find occupied ports** on the current machine.

 **Docker Ports in Use**

    
    
    #! /bin/bash
    #
    # Docker Containers: Find Occupied Port Numbers
    # ======================================================================
    # Find out what port numbers are used by Docker on this host.
    # ======================================================================
    
    sudo docker ps | perl -n -e ' m/0.0.0.0:(\d+)/; print $1 . "\n";' | sort -u

