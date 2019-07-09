---
explains: How to incorporate logging to your applications and how to visualize this data
---

# How we set up logging and monitoring

## Introduction

At Datapunt new applications, websites and data sources are released every month. To be able to monitor the use of these services, and to see the performance of our products, we use a standardised format for logging. To ensure scalability, up time monitoring, performance monitoring and error monitoring, some basic data needs to be logged by all applications. This guide contains instructions on how logging is implemented in our software.

## Frontend logging

All user statistics are logged in Matomo, formerly named Piwik. This web application monitors visits, unique visitors, visited pages, their urls, downloads, bounce rates, et cetera. It is fairly easy to implement these basic measurements by placing a small piece of Javascript on your site. You can find [instructions](https://developer.matomo.org/guides/tracking-javascript-guide){:target="_blank"} here. 

There are also possibilities to create custom events for every click or action that's available on your website, set goals and measure their conversions, create custom variables and dimensions, manage privacy and security and more. Some excellent middleware has been developed for these functionalities which are going to be released as generic components shortly in [this repo](https://github.com/Amsterdam/matomo){:target="_blank"}.

The log files are kept on our own servers and can be called either through [Matomo's API](https://developer.matomo.org/api-reference/reporting-api){:target="_blank"} or visualised in [Matomo's dashboarding tool](http://piwik.datapunt.amsterdam.nl){:target="_blank"}.

## Backend logging
On an application level every API call is logged in JSON format containing the following information:

* Frontend Name (which site/cluster called the API)
* Backend Name (which backend process does the API call)
* API endpoint (which functionallity called the API, mapclick, get request, et cetera)
* Http response status
* Time active
* Raw request line (depending on privacy sensitivity of the specific application)
* Correlation ID (using [Zipkin](https://zipkin.io/){:target="_blank"})

All the logs are then picked up by logstash/filebeat/elasticsearch. They can be inspected, aggregated and visualised in [Kibana](http://logs.data.amsterdam.nl){:target="_blank"}. Standard visualisations and dashboards are available on request from team Service Delivery.  

## Error monitoring
Error monitoring can be done through the [Kibana](http://logs.data.amsterdam.nl){:target="_blank"} interface. Some developers also add a Sentry config to get notified when and where errors are occuring.

## Up time monitoring
We use up time robot to check if our applications are up and running. Adding an empty file to YOUR_URL/status/health on your site allows team Basis to add a health check for your site to the uptimerobot config.

