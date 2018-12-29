# Public Docker Registries and Sample Images

This page points to public **Docker image** files to use as starting points.
Each **image** may be a **Dockerfile's** **FROM** declaration. In particular,
it is concerned with creating **WSGI Django services**.

## Apache and MOD WSGI Images

**Apache 2** and **MOD WSGI** provide a high volume Webserver to run Python
**WSGI scripts** or **Django servers**. The author of **mod_wsgi** has created
**Docker images** to streamline this.

Reference | Description 
----------|------------
[Tutorial on Docker and WSGI](http://blog.dscpl.com.au/2014/12/hosting-python-wsgi-applications-using.html) | _Graham Dumpleton's_ tutorial on his Apache/mod_wsgi Docker Images
[Docker Images](https://hub.docker.com/r/grahamdumpleton/mod-wsgi-docker/) | Docker images support **python 2.7** and **python 3.5** versions

## CentOS Docker Images

These **Docker images** have **centos:7** as a _base image_ and are suitable
to **docker run** in a **CentOS 7.x** host server.

Reference | Description 
----------|-------------
[CentOS Dockerfiles](https://github.com/CentOS/CentOS-Dockerfiles) | Many **Dockerfile** projects to build common **CentOS** services
[MariaDB Docker Image](https://hub.docker.com/r/centos/mariadb/)   |  Run a **MariaDB** SQL database server on **Docker**                      

## Selenium Grid Images

**Selenium** can be run as a **grid** where several **nodes** work behind a **hub** service.
Each **node** handles an **operating system** and supports _one or more_ **browser WebDrivers**.

Reference | Description                                             
----------|------------
[Docker Selenium](https://github.com/SeleniumHQ/docker-selenium) | Docker images for a Selenium **hub** and separate **nodes** for each browser brand 
[Selenium Grid with Docker](http://testdetective.com/selenium-grid-with-docker/) |  A tutorial on starting **Selenium Grid** Docker images
[Using Docker Custom Nodes](http://testdetective.com/selenium-grid-with-docker-custom-nodes/) |  Customize the **Node's** Docker images with more browsers, etc
