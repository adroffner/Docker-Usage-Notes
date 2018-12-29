There is an
![](/plugins/servlet/confluence/placeholder/error?i18nKey=editor.placeholder.broken.link&locale=en_GB&version=2)
to store **images** within the **OCNP** and deploy **Docker** services. This
page describes how to **docker push** or **docker pull** a service **image**
in the registry.

## Create an Image Tag

Use **docker tag** to name an image properly. Otherwise it will not be
accepted into the **registry**. Construct the image tag out of the **Docker
Tagging Terms** listed below that are specific to **BizOps**.

 **Create an Image Tag for the Registry**

    
    
    # Tagging Format:
    $ docker tag <image ID> registry/namespace/image_name:tag
    
    # Example: Only image_name & tag will be different each time.
    # image_name = centos7-elasticsearch
    # tag = latest
    $ docker tag 12e2DRF11e dockerhub.example.com:5100/com.example.namespace/centos7-elasticsearch:latest

### **** Docker Tagging Terms

There are several **terms** needed to contract _tagging_.

Term                                            | Value                          | Description                                     
------------------------------------------------|--------------------------------|-------------------------------------------------
**username** or mechID                          |  m06637                        | **username** who logs into the **registry**     
services hostname                               | namespace.example.com          | the common services **hostname**                
without any port number                         
**registry** server                             |  dockerhub.example.com:5100    | **Docker registry**                             
server and port number                          
Docker **namespace**                            |  com.example.namespace             | Set **namespace** to the reverse                
of hostname                                     
**image_name**                                  |                                
                                                
_specific to image_                             
                                                
                                                |                                
                                                
Set the **image name** to a descriptive name ** 
**                                              
                                                
**tag**                                         | _release tag_                  |  Set the **release tag** to a version number or 
**latest**                                      


## Docker Login to Registry

Employees must **login** to the registry and store credentials. The example
below shows a shared **username** login to the Docker registry.

 **BizOps Docker Login**

    
    
    docker login -u username@namespace.example.com -p <password> dockerhub.example.com:5100

## Docker Push

Use **docker push** to add the image to the registry. Always **Create an Image
Tag** first that matches the registry.

 **Push Tagged Image to Registry**

    
    
    docker tag <image ID> dockerhub.example.com:5100/com.example.namespace/centos7-elasticsearch:latest
    docker push  dockerhub.example.com:5100/com.example.namespace/centos7-elasticsearch:latest

## Docker Pull

Use **docker pull** get an image from the registry.

 **Pull Image from Registry**

    
    
    docker pull dockerhub.example.com:5100/com.example.namespace/centos7-elasticsearch:latest

## Searching for Docker Images

**Search the Docker registry** for existing images. This can prove which
versions of an **image** are truly pushed there. The **registry host** &
**namespace** must be provided,
**dockerhub.example.com:5100/com.example.namespace/** , or the _default_ public
registry will get searched (not ours).

 **Find Docker Images**

    
    
    $ docker search dockerhub.example.com:5100/com.example.namespace/docker_codb_api
    
    NAME                                                                                 DESCRIPTION   STARS     OFFICIAL   AUTOMATED
    dockerhub.example.com:5100/com.example.namespace/docker_codb_api:0.6b4-318-gee46012                 0                    
