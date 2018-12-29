This page explains how to run and manage **Docker Image** within a
**container**. It focuses on server images such as Web servers or databases.

Running: Containers vs. Images

**Docker** has two ways to start up a server depending on whether there is
already a **container** or only an **image**.

Docker Command      | Description                                                    
--------------------|----------------------------------------------------------------
docker run          | **Run** an **image** and create a new **container** for it     
docker start        | **Start** an existing **container** with the same **image** as 
**docker run** used 


## Run Image in the Background

It is best to run a **Docker image** in a background or _daemon_ **container**
process.

  * See [this example](https://linuxconfig.org/how-to-start-a-docker-container-as-daemon-process)

### Run Image in a New Named Container

Use **docker run -d** to invoke a new **container** in _daemon mode._ The
**container** acts like another server inside the host machine and has
terminal access.

 **Run Docker in Daemon Mode**

    
    
     $ docker run -d -p 8000:80 --name my-running-app my-python-app

### Terminal Access

Enter a **container** shell using the **docker exec** command on
**/bin/bash**. In fact, **docker exec** works on any Linux command.

 **Docker Shell Access**

    
    
    $ docker exec -it my-running-app /bin/bash

### Shut Down the Container

Finally, **docker stop <container id>** shuts down the **container**. Use
**docker ps** to find the **CONTAINER ID** code.

 **Shut Down a Docker Container**

    
    
    $ docker ps
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
    07facbc3f32d        72bd00a7df6e        "mod_wsgi-docker-star"   7 seconds ago       Up 6 seconds        0.0.0.0:8001->80/tcp   condescending_khorana
    
    $ docker stop 07facbc3f32d
    07facbc3f32d

## View Docker Processes

Use **docker ps,** similar to the Linux **ps** command, to view **container**
processes. Unlike Linux, **docker ps** shows both _running_ and _exited
(stopped)_ **containers**.

### Show Running Containers

Show only _running_ **containers** including **image ID** and the _port
mappings_ from the host machine.

 **Show Running Container(s)**

    
    
     $ docker ps
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
    07facbc3f32d        72bd00a7df6e        "mod_wsgi-docker-star"   7 seconds ago       Up 6 seconds        0.0.0.0:8001->80/tcp   condescending_khorana
    

### Show All Containers

Show any **containers** , _running_ , _exited_ , or otherwise.

**Show All Containers**

    
    
    $ docker ps -a
    ...

### List Occupied Port Number

Running **containers** expose a service **port** number, which **must** be
unique. This **BASH script** lists all the **ports** occupied on the current
**host** machine **.**

 **List Occupied Ports**

    
    
    #! /bin/bash
    #
    # Docker Containers: Find Occupied Port Numbers
    # ======================================================================
    # Find out what port numbers are used by Docker on this host.
    # ======================================================================
    
    docker ps -a | perl -n -e ' m/0.0.0.0:(\d+)/; print $1 . "\n";' | sort -u

