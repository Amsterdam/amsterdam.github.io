---
explains: The style guide to the way we organize our Python back-end projects
---

# Python backend projects

## Introduction
This document describes the common practices that are used in our Python backend projects.
It is not meant as an encompassing development standards document.
Within the backend team developers are free to choose the best tool for the job.

## How we use docker and docker-compose

A lot of the [open source code software of the City of Amsterdam](https://github.com/Amsterdam) uses Docker containers.
Separate tasks are normally organised in separate Dockers.

In general we follow common community guidelines:
- [Dockerfile best practices](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)
, including multi-stage builds

Preferably use [docker-ce](https://www.docker.com/community-edition)
and [docker-compose](https://docs.docker.com/compose/), most recent version

`.dockerignore` files are used to exclude files that are not relevant to the build.
Ideally this file starts by ignoring everything (`*`) and then explicitly add the files that belong to the build
by means of exceptions (e.g. `!**\*.py` to include all python source files).
Most often you will however find .dockerignore files that only specify files that are not part of the build. 

## How we use Python

See [Python Style Guide](style-guide-python.md)

## What you can expect to find in our project structure

* readme
* license
* services:

  * each defined in a separate folder at the root level of the project
  
  * each having separate sources and tests folders
  
  * each having a `Dockerfile` with a corresponding `.dockerignore`
  
  * each having a `setup.py` and/or a `requirements.txt` file to install the package 

* `docker-compose.yml`
* `.gitignore`
* jenkins or similar ci yaml to configure the continuous build and integration
* `.jenkins` folder
* `.swarm` folder

## How we test

All of our projects require (unit) tests which are integrated in the continuous build process.

For testing we prefer using [pytest](https://docs.pytest.org/), following its corresponding [good practices](https://docs.pytest.org/en/latest/goodpractices.html)

However you may find the use of unittest in some (older) projects.

Code coverage is normally not checked.
Absolute code coverage requirements and enforcement thereof exist only in very rare cases.

## How we assure our code quality

All code is reviewed by a colleague and subsequently accepted in the acceptance environment, before it is released to the production environment.

Deployment to production is a manual action in the Continuous Integration (CI) environment.

Linting tools ([pylint](https://www.pylint.org/), [flake8](http://flake8.pycqa.org/), [pycodestyle](https://pypi.python.org/pypi/pycodestyle), ...) and the inclusion of these checks in the CI cycle are rarely done in our projects.
Most of the linting is expected to be done by the IDE.
Code quality checks are normally not part of the build process.CI

## How we build our API's

Our API's are documented using [swagger](https://swagger.io/). Each project is able to serve a swagger json or yaml file.
The endpoint is included in the [catalog](https://github.com/Amsterdam/catalog) project and so exposing it to our clients.

Swagger first is preferred. This means that the swagger specification determines the API service.

Common practice is however to start with the development of the API and generate or write the swagger documentation afterwards.

## Which frameworks we use

[Django](https://www.djangoproject.com/) and [Flask](http://flask.pocoo.org/) are used alternately. Projects that are tightly connected to databases normally use the Django framework.
Other (mostly smaller) projects often make use of the Flask framework.

In recent projects the aiohttp asynchronous HTTP client/server is used.

    Recently we also use [golang](https://golang.org/). The specific practices for these projects will be described in a seperate guide.

## How we share code between our projects

We are in the process of packaging our shared code. Links to relevant packages will be included in this guide when they become available.

However, you will also find shared code that has been included in other projects by simply copying its contents.

## Template project

A real template project that is used to bootstrap a new project does not exist within our repository.
There exists however a project that serves more or less as our showcase project: [Monumenten](https://github.com/Amsterdam/monumenten).
The setup and layout from this project can be taken as a starting point for new projects.

## Which DataBase Management System (DBMS) we use

[PostgreSQL](https://www.postgresql.org/). In Flask projects the [SQLAlchemy](https://www.sqlalchemy.org/) library is used to access the database.

## How we use github

### Issues
Issues are registered in Jira or Taiga. Git issues are not used.
Other github users will normally not be able to check for any solved or open issues.
Neither is any procedure in place to respond to new issues that are registerd in github.

### Feature branches
Normally not used, all code resides in one branch; the master branch.

### Pull requests
Pull requests are rarely used. Updates are normally directly pushed onto the master branch.

### Protected branches
Branches like master or development are not protected against direct updates.

### Reviews
Reviews are on the basis of commits.
A review task is taken from Jira or Taiga.
In the review task the reference to the commit is included.
The commit description and the description of the original task is taken as input for the review.
There is normally no description of how the modification can be tested.

### Merge or rebase
Common practice is that commits are rebased.
Rebasing not only keeps the master history clean,
it also ensures that each commit in the master history has been tested, reviewed and works.
