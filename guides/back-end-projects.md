---
explains: The style guide to the way we organize our back-end projects
---

# How we use docker and docker-compose

A lot of the software we make at City of Amsterdam uses docker containers.

In general we follow the common community guidelines:
- [Dockerfile best practices](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)
, including multi-stage builds

Preferably use [docker-ce](https://www.docker.com/community-edition)
and [docker-compose](https://docs.docker.com/compose/), most recent version

.dockerignore files are used to exclude files that are not relevant to the build.
Ideally this file starts by ignoring everything (`*`) and then explicitly add the files that belong to the build
by means of exceptions (e.g. `!**\*.py` to include all python source files).
Most often you will however find .dockerignore files that only specify files that are not part of the build 

# How we use Python

See [Python Style Guide](style-guide-python.md)

# What you normally can expect to find in our project structure

* readme
* license
* services

  each defined in a seperate folder at the root level of the project
  
  each having a seperate service sources and tests folder
  
  each having a Dockerfile
  
  each having a setup.py and/or a requirements.txt file to install the package 

* docker-compose.yml
* .gitignore
* jenkins or similar ci.yml to configure the continuous build and integration
* .jenkins
* .swarm

# How we test

For all our projects it is a requirement that tests are available and are integrated in the continuous build process.

For testing we prefer using pytest.

However you may find the use of unittest in some (older) projects.

Code coverage is normally not checked.
Absolute code coverage requirements and enforcement thereof exist only in very rare cases.

# How we assure our code quality

Linting tools (pylint, flake8, pep8, ...) and the inclusion of these checks in the CI cycle are rarely done in our projects.
Most of the linting is expected to be done by the IDE.
Code quality checks are normally not part of the build process.

# How we build our API's

Our API's are documented using swagger. Each project is able to serve a swagger json or yaml file.
The endpoint is included in the [catalog](https://github.com/Amsterdam/catalog) project and so exposed to our clients.

Swagger first is preferred. This means that the swagger specification determines the API service.
For an example of this appraoch see [ADD LINK]()

# Which frameworks we use

Django and Flask are used alternately. Projects that are tightly connected to databases normally use the Django framework.
Other projects often make use of the Flask framework.

In recent projects the aiohttp HTTP client/server is used.
This framework has been extended with HAL json functionality in the [ADD LINK]() project.

# Which databases we use

Postgres. In Flask projects the sqlalchemy library is used to access the database.

# How we use github

## Issues
Issues are registered in Jira or Taiga. Git issues are not used.
Other github users will normally not be able to check for any solved or open issues.
Neither is any procedure in place to respond to new issues that are registerd in github.

## Pull requests
Pull requests are normally not used. Updates are normally directly pushed in the master branch.

## Protected branches
Branches like master or development are not protected against direct updates.

## Reviews
Reviews are on the basis of commits.
A review task is taken from Jira or Taiga.
In the review task the reference to the commit is included.
The commit description and the description of the original task is taken as input for the review.
There is normally no description of how the modification can be tested.

## Merge or rebase
The choice for merge or rebase is free.
Because of the fact that developers work mostly alone in a repository this does not unnecessary complicate the commit history.
