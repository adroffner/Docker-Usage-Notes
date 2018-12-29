# Docker Registry: Pushing and Pulling Images

Use a **Docker Registry** server to store **images** and deploy **Docker** services.
This page describes how to use **docker push** or **docker pull** a service **image**
in the registry.

## Create an Image Tag

Use **docker tag** to name an image properly. Otherwise it will not be
accepted into the **registry**.

Construct the image tag out of the **Docker Tagging Terms** listed below.

 **Create an Image Tag for the Registry**
    
    # Tagging Format:
    $ docker tag <image ID> registry/namespace/image_name:tag
    
    # Example: Only image_name & tag will be different each time.
    # image_name = centos7-elasticsearch
    # tag = latest
    $ docker tag 12e2DRF11e dockerhub.example.com:5100/com.example.namespace/centos7-elasticsearch:latest

### **** Docker Tagging Terms

There are several **terms** needed to contract _tagging_.

Term | Value | Description                                     
-----|-------|------------
**username** |  user001 | **username** who logs into the **registry**     
services hostname | namespace.example.com | the common services **hostname** without any port number
**registry** server |  dockerhub.example.com:5100 | **Docker registry** server and port number
Docker **namespace** |  com.example.namespace | Set **namespace** to the reverse of hostname
**image_name** | _specific to image_ | Set the **image name** to a descriptive name
**tag** | _release tag_ |  Set the **release tag** to a version number or **latest**

## Docker Login to Registry

Users must **login** to the registry and store credentials.
The example below shows a shared **username** login to the Docker registry.

 **Docker Login**

    docker login -u username@namespace.example.com -p <password> dockerhub.example.com:5100

## Docker Push

Use **docker push** to add the image to the registry. Always **Create an Image Tag** first
that matches the registry.

 **Push Tagged Image to Registry**

    docker tag <image ID> dockerhub.example.com:5100/com.example.namespace/centos7-elasticsearch:latest
    docker push  dockerhub.example.com:5100/com.example.namespace/centos7-elasticsearch:latest

## Docker Pull

Use **docker pull** get an image from the registry.

 **Pull Image from Registry**

    docker pull dockerhub.example.com:5100/com.example.namespace/centos7-elasticsearch:latest
