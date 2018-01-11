---
explains: A working guide for analists in the DataLab 
---

# Setting up

## Introduction
This document describes a common workflow for the analists how to get up-and-running and have a quickstart for their 
particular projects. It is not meant as an encompassing document but rather as way a standardized proposal to work and save time.

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

## Where do we store code

Every project should share reproducible code. We distinguish between sensitive projects (like for privacy sensitive projects) and 
projects with data that is not particularly sensitive.

- If your project contains contains sensitive code push your code to https://git.datapunt.amsterdam.nl/
- otherwise to the relevant code repository on https://github.com/amsterdam
- We also publish code snippets as gists on https://gist.github.com publicly but in that case make sure you add the following tag 
  to the snippet: #AmsterdamCityData




