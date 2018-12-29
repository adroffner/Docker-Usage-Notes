# Building Docker Images and Linux Distributions

A **Docker** image must have an **operating system** provided by the _base image_.
This must be a **Linux distribution** when the **host** **operating system** is itself **Linux**.

_Linux based_ images **should share the same Linux kernel version** as the
**host OS** running **docker-machine**. However, it **need not be the same
distribution**.

# Linux Distributions

There are only a few distinct **Linux distributions** where the **package manager** determines the kind.

Linux Distribution                                                         | Image Size                                                  | Package Manager                   | C/C++ Linkage |    
Description                                                                
---------------------------------------------------------------------------|-------------------------------------------------------------|-----------------------------------|---------------|----
**alpine Linux**                                                           | _small_                                                     | **[Search                         
for](https://pkgs.alpinelinux.org/packages)apk** _alpine package manager_  |                                                             
**muslc** linkage                                                          | **alpine Linux** is a _very small_ **busybox** operating    
system and the resulting **image** files are small                         
**CentOS**                                                                 | _large_                                                     | **RPM** _Red Hat package manager_ | **GCC glibc** 
linkage                                                                    | **CentOS** (or **Fedora** , **Red Hat** , **RHEL** ) is the 
_largest_ one and produces **fat** **image** files                         
**Debian** **Slim**                                                        | _medium_                                                    | **[Search                         
for](https://www.debian.org/distrib/packages#search_packages)aptitude** or 
**apt-get**                                                                | **GCC glibc** linkage                                       | **Debian Slim** is a _lighter_    
**Debian** footprint, but compiles the same C-source as **CentOS**         


## Building Smaller Images

Choosing the right **Linux distribution** can make **Docker** build much
smaller images, **megabytes instead of gigabytes**. Yet, there is a _trade
off_ between **size** and the **programmer's time** , where familiarity with a
**distribution** makes the **Dockerfile** easier to write.

Some guideline on the **Linux distributions** is given here.

### alpine Linux

This one creates the **smallest** image, but the **operating system** is
**busybox** and **muslc** linkage. An **alpine** image may not build C/C++
code that the others can, and many **python3** libraries have a C-source
component.

### CentOS

This one creates the **largest** image, but _at AT &T_ it is **exactly the
same operating system** as the **host machine**. There is very little chance
the image has incompatible code. A programmer who has used **RHEL** and
**rpm** can write write a **Dockerfile** quickly.

### Debian Slim

This one creates _medium size_ images that are largely compatible with
**CentOS** , since they both use **glibc linkage**.Yet, the images are about
60% the size of a **CentOS** version.

# Example: Python3 WSGI Services

Each **Linux distribution** can create a **Python WSGI** **Webserver** using
**Apache 2** and the **mod_wsgi** module. Ideally, they should all load a
**Python** source project the same way. The **mod_wsgi-express start-server**
paradigm makes this easy.

Alpine Linux has no start-server

The **alpine linux** version of **python3-mod_wsgi** does not support
**mod_wsgi-express** and its **start-server** command. The **mod_wsgI** module
is installed, and functional, but **WSGI services** need **Apache .conf**
files made for them.

## MOD_WSGI Images

 **python3-mod_wsgi images**

    
    
    1    dockerhub.example.com:5100/com.example.namespace/alpine-python3-mod_wsgi:3.6.6
    2    dockerhub.example.com:5100/com.example.namespace/centos7-python3-mod_wsgi:3.6.6
    3    dockerhub.example.com:5100/com.example.namespace/debian-slim-python3-mod_wsgi:3.6.6

## Using start-server

Every **mod_wsgi-express start-server** enabled image just needs the
**python** code and a **start-server** script. The **start-server** below is
the **Dockerfile ENTRYPOINT=/home/bin/start-server.sh** to run a REST API
service.

 **Run start-server as Docker ENTRYPOINT**

    
    
    #! /bin/bash
    #
    # WFA OSSCWL Apache mod-wsgi service
    # =============================================================================
    
    WEB_USER="www-data" # Debian
    
    /usr/local/bin/mod_wsgi-express start-server \
        --user "${WEB_USER}" \
        --maximum-requests=250 \
        --access-log \
        --access-log-format "[OSSCWL-API][%>s] %h %l %u %b \"%{Referer}i\" \"%{User-agent}i\" \"%r\"" \
        --error-log-format  "[OSSCWL-API][%l] %M" \
        --log-to-terminal --log-level INFO \
        --url-alias /static static \
        --host 0.0.0.0 --port 8030 \
        --passenv http_proxy \
        --passenv https_proxy \
        --passenv no_proxy \
        --working-directory /home/app \
        --compress-responses \
        --application-type module osscwl_api.wsgi

