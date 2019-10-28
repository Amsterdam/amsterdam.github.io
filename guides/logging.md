---
explains: How to incorporate logging to your applications and how to visualize this data
---

# How we set up logging and monitoring

## Introduction

At Datapunt new applications, websites and data sources are released every month. To be able to monitor the use of these services, and to see the performance of our products, we use a standardised format for logging. To ensure scalability, up time monitoring, performance monitoring and error monitoring, some basic data needs to be logged by all applications. This guide contains instructions on how logging is implemented in our software.

For technical details about logging and monitoring in general, including notes on frontend- and backend logging, reporting and dashboarding, Amsterdam officials can view [the general logging and monitoring dokuwiki](https://dokuwiki.datapunt.amsterdam.nl/doku.php?id=start:datapunt:beheren:logging_en_monitoring){:target="_blank"}.

## Frontend logging

All user statistics are logged in Matomo, formerly named Piwik. This web application monitors visits, unique visitors, visited pages, their urls, downloads, bounce rates, et cetera. It is fairly easy to implement these basic measurements by placing a small piece of Javascript on your site. You can find [instructions](https://developer.matomo.org/guides/tracking-javascript-guide){:target="_blank"} here. 

There are also possibilities to create custom events for every button click or action that's available on your website, set goals and measure their conversions, create custom variables and dimensions, manage privacy and security and more. Some excellent middleware has been developed for these functionalities which can be found in [this repo](https://github.com/Amsterdam/matomo-tracker){:target="_blank"}. 

The log files are kept on our own servers and can be called either through [Matomo's API](https://developer.matomo.org/api-reference/reporting-api){:target="_blank"} or visualised in [Matomo's dashboarding tool](http://analytics.data.amsterdam.nl){:target="_blank"}.

Further technical details and implementation choices specifically about [data.amsterdam.nl](https://data.amsterdam.nl){:target="_blank"} can be viewed by Amsterdam officials on [the sata and information dokuwiki](https://dokuwiki.datapunt.amsterdam.nl/doku.php?id=start:toepassingen:citydata:piwik){:target="_blank"}.

## Backend logging
On an application level every API call is logged in JSON format. The technical details can be found on [the general logging and monitoring dokuwiki](https://dokuwiki.datapunt.amsterdam.nl/doku.php?id=start:datapunt:beheren:logging_en_monitoring){:target="_blank"}.

All the logs are then picked up by logstash/filebeat/elasticsearch. They can be inspected, aggregated and visualised in [Kibana](http://logs.data.amsterdam.nl){:target="_blank"}. Standard visualisations and dashboards are available on request from team Service Delivery.  

## Error monitoring
Error monitoring can be done through the [Kibana](http://logs.data.amsterdam.nl){:target="_blank"} interface. Some developers also add a [Sentry](https://sentry.data.amsterdam.nl){:target="_blank"} config to get notified when and where errors are occuring.

## Up time monitoring
We use [Up Time Robot](https://uptimerobot.com){:target="_blank"} to check if our applications are up and running. Adding an empty file to YOUR_URL/status/health on your site allows team Basis to add a health check for your site to the uptimerobot config.

