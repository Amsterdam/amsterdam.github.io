---
explains: How we set up a docker environment for analysis
---


# How we create a docker environment for data analysis

# Setting up

## Introduction
This document describes a common workflow for the analists how to get up-and-running and have a quickstart for their 
particular projects using Dockers. It is not meant as an encompassing document but rather as way a standardized proposal to work and save time.

## Install procedure for a project. 

**install docker**
Depending on your OS, find install procedures here:
-for Ubuntu <a href="https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/"</a></br>
-for Mac: https://docs.docker.com/docker-for-mac/install/
-for windows: first check your OS version. For Windows users the 10 Home editions use Docker Toolbox, a Legacy desktop solution intended for older Mac and Windows systems that do not meet the requirements of Docker for Mac and Docker for Windows. It is recommended upgrading to newer applications, if possible and for Windows users to upgrade to PRO. Windows: https://docs.docker.com/toolbox/toolbox_install_windows/ . This toolbox run on Oracle VirtualBox VM and is therefore a lot slower than the following install solution. 
, Windows 10 PRO users: download Docker for Windows PC Community Edition from the Docker Store.  https://www.docker.com/docker-windows 
download and install <a href="https://www.docker.com">docker</a></br>

To get started with Docker, see the official [starting guide](https://docs.docker.com/get-started/)

## How we use docker and docker-compose

A lot of the [open source code software of the City of Amsterdam]((https://github.com/Amsterdam)) uses docker containers.
Seperate tasks are normally organised in seperate dockers.

In general we follow common community guidelines:
- [Dockerfile best practices](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)
, including multi-stage builds

Preferably use [docker-ce](https://www.docker.com/community-edition)
and [docker-compose](https://docs.docker.com/compose/), most recent version

`.dockerignore` files are used to exclude files that are not relevant to the build.
Ideally this file starts by ignoring everything (`*`) and then explicitly add the files that belong to the build
by means of exceptions (e.g. `!**\*.py` to include all python source files).
Most often you will however find .dockerignore files that only specify files that are not part of the build. 

**define a container with a dockerfile**
dockerfiles defines what goes into the container. start by creating an empty directory, change directories into the new directory (CD), and create a file called Dockerfile. 

The Dockerfile you need to build the postgres base instance can be found at https://github.com/Amsterdam/docker/blob/master/postgres/Dockerfile  

In the docker CL type: ```docker build -t projectname``` 

to run the image and build a container run: ```docker run -p 4000:80 projectname```
Check http://localhost:4000 for the rendering. If you are running Docker Toolbox on windows, use the docker Machine IP adress instead. You can find this one by docker-machine ip (http://192.168.99.100:4000/) f.i.

1) **build postgreSQL data base image**
Access to resources like networking interfaces and disk drives is virtualized inside this environment, isolated from the rest of your system, so you have to map ports to the outside world, and be specific about what files you want to “copy in” to that environment.

```
git clone https://github.com/Amsterdam/schoonmonitor.git schoonmonitor
cd schoonmonitor
docker-compose build database
docker-compose up database
```

This builds a postgres Image from the public repository of Docker Hub (https://hub.docker.com/r/amsterdam/postgres/)
based on a build context stored in the offical repository https://github.com/Amsterdam/docker. A build context is a Dockerfile and any files at a specific location. For an automated build, the build context is a repository containing a Dockerfile.
The docker postgres database can be found on localhost:5403

To start using servcies, you must initialize a swarm. See docs: https://docs.docker.com/engine/reference/commandline/swarm_init/#usage
```docker swarm init --advertise=addr 172.17.0.1``` : the docker engine targeted by this command becomes a manager in the newly created single-node swarm.

**build importer**

Instantiate a new docker client to import project specific data
general components include:
  - download_from_objectstore.py
  - etc....
  
Set the openstack config in auth.conf by using and renaming auth.conf-example and set the openstack password in your environment:
```
SET ENV EXTERNAL_DATASERVICES_PASSWORD = yourpassword
```
or on Unix
```
export EXTERNAL_DATASERVICES_PASSWORD = yourpassword
```

In the docker client run:

**docker-compose yaml file** 
The Compose file is a YAML file defining services, networks and volumes. The default path for a Compose file is ./docker-compose.yml.

## Where do we store code**

Every project should share reproducible code. We distinguish between sensitive projects (like for privacy sensitive projects) and 
projects with data that is not particularly sensitive.

- code should be pushed to github.com/amsterdam with the exception of privacy-sensitive projects that are hosted on our own closed git at git.datapunt.amsterdam.nl https://git.datapunt.amsterdam.nl/
- We also publish code snippets as gists on https://gist.github.com publicly but in that case make sure you add the following tag 
  to the snippet: #AmsterdamCityData
