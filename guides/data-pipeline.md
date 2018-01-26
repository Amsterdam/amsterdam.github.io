---
explains: The way we make reusable data etl pipelines
---

# How we create cleaned, reproducable data for use in projects and apps

At the City of Amsterdam we deal with many different types of structured and unstructered data.
Much of the data is not of high quality and are missing a lot of needed semantics to do proper analytics with.

This guide describes our workflow for creating a reproducable ETL data flow which we use to create better data for analytics and usage in dashboards and maps.

## First things first

We use a these principles:
- One City, one solution: meaning: We try to write ETL scripts which are the start for a more structural solution, not a one off.
- Create resuable code as [Open Source](track-open-source-health.md)
- Use [Git](https://git-scm.com) as version control
- Publish the code on [github.com/amsterdam](https://www.github.com/amsterdam) as a project with a clear [Readme](write-a-readme.md).
- Use [Docker](https://www.docker.com) to automate, using the [backend project methods](back-end-projects.md).
- Use [Python](https://www.python.org) as a scripting language for the processing steps. using this [python style guide](style-guide-python.md).
- Write [code for humans](https://amsterdam.github.io/guides/code-for-humans/).
- Use a [Postgres](https://www.postgresql.org) with [Postgis](http://postgis.net) extension [Docker image](https://hub.docker.com/r/amsterdam/postgres/) as a data storage and cleaning/merge solution.
- We always try to improve the data quality of the clients data supplier where possible by explaining and showing the benefits of integrating https://api.data.amsterdam.nl endpoints to use [basisregistraties](https://www.amsterdam.nl/stelselpedia/) to achieve the first principle.



<a href="/images/data-pipeline-flow-v2.png"><img src="/images/data-pipeline-flow-v2.png" width="800"></a>

<a href="https://www.draw.io/?lightbox=1&highlight=000000&edit=_blank&layers=1&nav=1&title=data_pipeline_v2.xml#Uhttps%3A%2F%2Fraw.githubusercontent.com%2Famsterdam%2Famsterdam.github.io%2Fmaster%2Fdata-pipeline-flow-v2.xml">edit xml with draw.io</a>.

## ETL workflow

The current roles within the City of Amsterdam are described here with which people and teams we collaborate with to get our data:
<a href="/images/data-pipeline-flowchart.png"><img src="/images/data-pipeline-flowchart.png" width="400"></a>

The workflow consist of 4 steps:
1. Getting the data
2. Stage the data
3. Clean the data
4. Combine the data

### 1. Getting the data

Much of the data is still recieved by mail in the form of database dumps as tabular or spatial file. That creates a dependancy of the availability of person on the sending and recieving end regarding adding new data to the pipeline.

To solve this an make automation possible, clients are asked to:

**A. API/web route**
1. Create an API token to access the api of the registration system and send the token by mail.
2. Send an API token by mail.
3. Send PHP login credentials by mail to use the API's.
4. If there is no api available: Ask the owner of the data to create an api on the registration system and help with the api output definitions.

**B. Database route**

5. Recieve an user account for a datamart connection and ask for a ip connection through Motiv if it is not yet available @datapunt.

**C. File delivery route**

6. Let the client upload a database dump periodically to the objectstore with a user/password.
7. Send the (database) dump by mail to the data analist.
8. Copy the dump on to a protected/encrypted USB stick on location.

Optionally:
Send the ip ranges of our organisation to the application maintainers.

**Responsibility of the data analist/engineer:**

1. Store the token/login in the password manager
2. Store the userlogin/password in the password manager of the project or team
3. Store the dump on the objectstore


### 2. Staging the data

At the city of Amsterdam we work a lot with spatial data. That's why we use Postgres with the Postgis extention often to combine, enrich and clean spatial data. 

To load the data into the database we use python in a Docker container to create a resuable and production viable import for every project.

A typical flow will look like this:

1. Setup the credentials as environment variables.
2. Login to objectstore or api.
3. Download all records by looping through the API objects, downloading from the objectstore or loading them from a datamart.
4. Save the files/objects in dataframe or dict and do some preliminary data cleanup.
5. Set the schema if needed.
6. Store the dataframe/dict in the postgres database in a schema with the name of the project.
7. Add additional tables for semantic enrichment, like neighborhood areas or addresses.
8. Create a view for use for analyis or further usage in Service backends like the Django Rest Framwork or programs like Tableau Desktop. 
