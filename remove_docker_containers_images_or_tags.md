# Remove Docker Containers Images or Tags

**Docker** stores **containers** and **image** files within the local registry.
This page explains how to remove local **Docker images** or **containers**.

## Removing old Containers or Images

Over time, **Docker** files accumulate and must be deleted. For example,
**containers** have **exited** when they stop, and may be removed.

Docker Command                       | Description                                  
-------------------------------------|----------------------------------------------
**docker rm** CONTAINER-ID ...       | Remove the **containers** matching the ID list
**docker rmi** IMAGE-ID ...          | Remove the **images** that match these IDs
**docker network rm** NETWORK-ID ... | Remove the closed **networks** that match these IDs
**docker volume rm** VOLUME-ID ...   | Remove the container disk **volumes** that match these IDs

###  Examples

**Remove Containers that were Created but Never Used**

    $ docker rm $(docker ps -q -f status=created)

**Remove Containers that Exited**

    $ docker rm $(docker ps -q -f status=exited)

**Remove Dead Containers**

    # Dead containers require the "-f" forced flag and may still leave orphaned volumes, etc.
    docker rm -f $(docker ps -a -q -f "status=dead")

**Remove Images that are Dangling <None>**

    $ docker rmi $(docker images -q -f "dangling=true") 

## Untag Images without Removal

Strangely, **docker rmi** is also used to **untag** an **image** file without deleting the image.
Suppose there are multiple **tags** on the same **IMAGE ID**. Use the command below to have only one tag.

 **Untag a Docker Image**

    $ docker images
    REPOSITORY                                                             TAG                 IMAGE ID            CREATED             SIZE
    ...
    dockerhub.example.com:5100/com.example.namespace/centos7-elasticsearch      latest              1eccd8ead98c        10 weeks ago        720.3 MB
    com.example.namespace/centos7-elasticsearch                                          5.1.1               1eccd8ead98c        10 weeks ago        720.3 MB
    com.example.namespace/centos7-elasticsearch                                          latest              1eccd8ead98c        10 weeks ago        720.3 MB
    
    $ docker rmi com.example.namespace/centos7-elasticsearch:5.1.1
    Untagged: com.example.namespace/centos7-elasticsearch:5.1.1
    
    $ docker rmi com.example.namespace/centos7-elasticsearch:latest
    Untagged: com.example.namespace/centos7-elasticsearch:latest

## Removing an Image with Multiple Tags

**Docker** will not **remove** an **image** that has **multiple tags**.
To remove the **image ID** , every **tag** name, except one, must be removed from the **image ID**.
Then, the **image** may be **removed by ID**.

**Unable to Delete**

    # Image ID 9908489e35a0 has multiple tags.
    $ sudo docker images | grep osscwl_rest_api
    dockerhub.example.com:5100/com.example.namespace/osscwl_rest_api               0.6b4-83-g8803c2f   e00ff5df540d        40 hours ago        1.041 GB
    dockerhub.example.com:5100/com.example.namespace/osscwl_rest_api               0.6b4-28-ga68797a   9908489e35a0        2 weeks ago         1.041 GB
    dockerhub.example.com:5100/com.example.namespace/osscwl_rest_api               0.6b4-71-g341db96   9908489e35a0        2 weeks ago         1.041 GB
    
    # Docker will not let us delete this image by ID.
    $ sudo docker rmi 9908489e35a0
    Failed to remove image (9908489e35a0): Error response from daemon: conflict: unable to delete 9908489e35a0 (must be forced) - image is referenced in one or more repositories
     
    # First, untag the image...select either tag to remove.
    $ sudo docker rmi dockerhub.example.com:5100/com.example.namespace/osscwl_rest_api:0.6b4-71-g341db96
    Untagged: dockerhub.example.com:5100/com.example.namespace/osscwl_rest_api:0.6b4-71-g341db96
     
    # Now, the image ID has ONE tag associated with it; remove the image now.
    [user@host ~]$ sudo docker rmi 9908489e35a0
