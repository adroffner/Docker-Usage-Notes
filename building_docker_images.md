# Building Docker Images

This page has notes on how to build a new **Docker image** before **running it in a container**

# Dockerfiles

The official [Dockerfile Reference page](https://docs.docker.com/engine/reference/builder/) lists the many
commands used to build **images**.

# Git Repository

My **Git repositories** store some **docker build** projects. This is a good place to see some examples.

# Building with a Proxy

Sometimes the **Dockerfile** cannot run package managers, e.g. **pip**, **apt-get**, or **yum**,
because **docker** is behind a firewall. In this case, an **HTTP proxy** is usually needed,
 and can be a **\--build-arg**.

## **Docker Build with a Proxy**

    # The current directory has the Dockerfile and source code.
    $ docker build -t $IMAGE_NAME ./ \
         --build-arg http_proxy=$http_proxy \
         --build-arg https_proxy=$https_proxy

