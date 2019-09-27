---
description: >-
  This document describes the architecture of the software that processes data
  and runs the Open Targets Platform.
---

# Infrastructure

All software developed by the Open Targets Core Team is available at: [https://github.com/opentargets](https://github.com/opentargets)

## Stack overview

* Data Pipeline - a custom Python2 based data pipeline that fetches data from public locations, process and loads them to the storage backend. The Pipeline is optimised for use of multiple cores in a single machine.
* Storage Backend - Storage is handled using Elasticsearch. The Data Pipeline handles a large amount of data during the processing steps. Elasticsearch stores data used by the REST API. Redis is also used as a cache.
* API - A Python2 Flask-based REST api that queries Elasticsearch to retrieve subset data from JSON documents and enable faceted search behaviour in the web app.
* Web App - An AngularJS based front end deployed at [www.targetvalidation.org](http://www.targetvalidation.org) that allows browsing the data with a user friendly data mining workflow enhanced with rich visualisations for the data. The Web App also acts as a data integration layer for data served by third-party APIs, some of which are behind a NGINX reverse-proxy.

Note: Web App & API are migrating to React and GraphQL / Scala respectively.

## Data pipeline

The ETL Pipeline is built in Python2, and requires an Elasticsearch server as datastore and a Redis server to organise the workflow and to act as a fast local cache when needed. A Redis server can be created as needed using the redislite python package.  The Pipeline is designed to be run via Docker on a single machine every 2 months, as part of the regular release process.  


The Pipeline reads ingest data, and then stores a JSON representation of the data in Elasticsearch. The evidence data is stored in JSON files on Google Cloud Storage and are validated and processed into Elasticsearch. Annotation data is also downloaded and incorporated into Elasticsearch, primarily from Google Cloud Storage but in some cases from external services such as GitHub.  


In production the data pipeline is executed on a Google Cloud Platform VM with 32 CPU cores and 128GB RAM, and takes approximately 24-48 hours to complete the processing.  


## Storage backend

  
Elasticsearch is used as the main datastore. The key features are:

* Ingest and store a large amount of JSON in a distributed resilient architecture
* Our Workflow does not need support for transactions
* Index and search by any part of the JSON field. This is key for the facet search data exploration workflow implemented in the web app
* Quickly return a small subset of JSON documents, supporting well our most frequent queries. 

## **REST API**

The REST API is built in Python2 using Flask with the Flask-restful extension and acts as a thin layer around a set of elasticsearch queries and does not execute any CPU or memory intensive task.  


The REST API makes use of a local Redis instance for caching and can be created as needed using the redislite python package. The REST API endpoints are documented with the Open API \(formally Swagger\) standard and the latest version is available here: [https://www.targetvalidation.org/api/docs/swagger.yaml](https://www.targetvalidation.org/api/docs/swagger.yaml)  


In production this is deployed on a 2 CPU / 4GB single machine in a Docker container using uWSGI and behind an NGINX server acting as reverse proxy. This is replicated in three global locations \(EU, US, JP\) for redundancy and performance.

## Web App

The Web App is built with AngularJS and makes use of many D3 visualisation and third party components served from the BioJS initiative.

The Web App fetches most of the content from the REST API described above. Some content is retrieved from public databases, and in some cases they are accessed through a reverse proxy in the Web App NGINX server to resolve HTTPS CORS issues.

In production, it is hosted by Netlify, but is also available as a Docker container.

Note: Web App & API are migrating to React and GraphQL / Scala respectively.  
  


