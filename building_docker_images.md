This page has notes on how to build a new **Docker image** before
![](/plugins/servlet/confluence/placeholder/error?i18nKey=editor.placeholder.broken.link&locale=en_GB&version=2).

# Dockerfiles

The official [Dockerfile Reference
page](https://docs.docker.com/engine/reference/builder/) lists the many
commands used to build **images**.

# Git Repository

This **Git repository** stores some **docker build** projects. This is a good place to see some examples.

# Building with a Proxy

Sometimes the **Dockerfile** cannot run package managers, e.g. **pip** ,
**apt-get** , or **yum,** because **docker** is behind a firewall. In this
case, an **HTTP proxy** is usually needed, and can be a **\--build-arg**.

 **Docker Build with a Proxy**

    
    
    # The current directory has the Dockerfile and source code.
    $ docker build -t $IMAGE_NAME ./ \
         --build-arg http_proxy=$http_proxy \
         --build-arg https_proxy=$https_proxy

# More Details

The pages below go into **more detail** on specific skills to build a **Docker
image**.

Unable to render {children}. This macro only works on pages.

