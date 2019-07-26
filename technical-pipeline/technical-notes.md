---
description: >-
  This page summarises the key technical revisions made to platform code to
  improve and streamline the full stack code in line with major releases
  scheduled to incorporate new data and features.
---

# Technical notes

## **19.06**

### **Release synchronised with:**

EFO 2.106 \(March 2019 - final release of Version 2\)

Ensembl 96 \(Apr 2019\)

### Updated docker images:

* [quay.io/opentargets/mrtarget:19.06.4](https://quay.io/repository/opentargets/mrtarget?tag=19.06.4&tab=tags)
* \*\*\*\*[quay.io/opentargets/rest\_api:19.06.4](https://quay.io/repository/opentargets/rest_api?tag=19.06.4&tab=tags)
* [quay.io/opentargets/webapp:19.06.4](https://quay.io/repository/opentargets/webapp?tag=19.06.4&tab=tags)

### Pipeline configuration file:

* \*\*\*\*[https://storage.googleapis.com/open-targets-data-releases/19.06/input/mrtarget.data.19.06.yml](https://storage.googleapis.com/open-targets-data-releases/19.06/input/mrtarget.data.19.06.yml%20) 

### Release highlights:

Blog: [http://blog.opentargets.org/2019/06/28/open-targets-platform-release-19-06-is-out ](http://blog.opentargets.org/2019/06/28/open-targets-platform-release-19-06-is-out%20)

Release notes: [https://docs.targetvalidation.org/release-notes](https://docs.targetvalidation.org/release-notes)

### Technical release information:

* Drug index implementation Phase I: [https://github.com/opentargets/platform/issues/451](https://github.com/opentargets/platform/issues/451)
* Pipeline
  * Customisable elasticsearch configuration  [https://github.com/opentargets/platform/issues/532](https://github.com/opentargets/platform/issues/532)
* REST API
  * Remove GProfiler from proxy [https://github.com/opentargets/platform/issues/437](https://github.com/opentargets/platform/issues/437)
* Webapp
  * Redesign drug profile page using new API endpoints created as part of drug index project Phase I [https://github.com/opentargets/platform/issues/564](https://github.com/opentargets/platform/issues/564)
  * Increase limit of API call for drugs evidence to 10,000 and adjustments made to layout if more than 10,000 evidence strings available [https://github.com/opentargets/platform/issues/589](https://github.com/opentargets/platform/issues/589)
  * Improvements to data download content and format for drugs tables
    * [https://github.com/opentargets/platform/issues/605](https://github.com/opentargets/platform/issues/605)
    * [https://github.com/opentargets/platform/issues/618](https://github.com/opentargets/platform/issues/618)
  * Supplementary explanations for Similar Targets and Similar Diseases tabs [https://github.com/opentargets/platform/issues/590](https://github.com/opentargets/platform/issues/590)
  * Inclusion of additional data table for inclusion of target safety data [https://github.com/opentargets/platform/issues/609](https://github.com/opentargets/platform/issues/609)

## **19.04**

### Updated docker images:

* [http://quay.io/opentargets/mrtarget:19.04.5](http://quay.io/opentargets/mrtarget:19.04.5)
* [http://quay.io/opentargets/rest\_api:19.04.5](http://quay.io/opentargets/rest_api:19.04.5)
* [http://quay.io/opentargets/webapp:19.04.5](http://quay.io/opentargets/webapp:19.04.5)

### Pipeline configuration file:

* [https://storage.googleapis.com/open-targets-data-releases/19.04/input/mrtarget.data.19.04.5.yml](https://storage.googleapis.com/open-targets-data-releases/19.04/input/mrtarget.data.19.04.5.yml)

### Release highlights:

Blog: [http://blog.opentargets.org/2019/05/01/open-targets-platform-release-19-04-is-out/](http://blog.opentargets.org/2019/05/01/open-targets-platform-release-19-04-is-out/)

Release notes: [https://docs.targetvalidation.org/release-notes](https://docs.targetvalidation.org/release-notes)  


### Technical release information:

* Pipeline
  * Updated documentation \([https://github.com/opentargets/data\_pipeline/blob/19.04.5/README.md](https://github.com/opentargets/data_pipeline/blob/19.04.5/README.md)\) improvements to clarify essential gene plugins and evidence json schema versioning
  * Replace external API with frozen files to improve reproducibility [https://github.com/opentargets/platform/issues/325](https://github.com/opentargets/platform/issues/325)
  * Use pypeln \([https://cgarciae.github.io/pypeln/](https://cgarciae.github.io/pypeln/)\) for multiprocessing instead of Redis [https://github.com/opentargets/platform/issues/361](https://github.com/opentargets/platform/issues/361) for improved reliability
  * many other improvements to improve reliability and performance of using multiple threads & processes
  * externalise url source to separate python package [https://github.com/opentargets/platform/issues/416](https://github.com/opentargets/platform/issues/416)
  * reduce default logging to info, and various minor logging improvements
  * remove delay between stages in Makefile which is a very minor performance improvement
  * new gene plugin to handle safety data
* REST API
  * Updated documentation \([https://github.com/opentargets/rest\_api/blob/19.04.5/README.md](https://github.com/opentargets/rest_api/blob/19.04.5/README.md)\) particularly using docker and SSL, and proxy
  * update swagger documentation to new platform API URL \([https://platform-api.opentargets.io/v3/platform/docs/swagger-ui](https://platform-api.opentargets.io/v3/platform/docs/swagger-ui)\). Note, configuring the API URL used by swagger is still open
  * minor configuration change to support crispr evidence
* Webapp
  * Option to auto expand certain data types e.g. for private data [https://github.com/opentargets/platform/issues/566](https://github.com/opentargets/platform/issues/566)
  * Customisation of "new" icon on panels [https://github.com/opentargets/platform/issues/511](https://github.com/opentargets/platform/issues/511)
  * Customisation of CSS styling and updated documentation on custom styling \([https://github.com/opentargets/webapp/blob/3.12.0/README.md](https://github.com/opentargets/webapp/blob/3.12.0/README.md)\)
  * Target safety data on the target profile page [https://github.com/opentargets/platform/issues/460](https://github.com/opentargets/platform/issues/460) - this is implemented directly on the page and not as a plugin \(like all the other sections\) as it is displayed only when there is relevant data.
  * New CRISPR cancer cell line data table on evidence page [https://github.com/opentargets/platform/issues/466](https://github.com/opentargets/platform/issues/466) - tables under “Pathways & systems biology” show when relevant.
  * Release notes now live in docs \(so those in the app are now deprecated\)

## **19.02**

### Updated docker images:

* [http://quay.io/opentargets/mrtarget:19.02.1](http://quay.io/opentargets/mrtarget:19.02.1)
* [http://quay.io/opentargets/rest\_api:19.02.1](http://quay.io/opentargets/rest_api:19.02.1)
* [http://quay.io/opentargets/webapp:19.02.1](http://quay.io/opentargets/webapp:19.02.1)  

### **Technical release information:** 

* JSON schema 
  * now separate schema all in one at: [https://raw.githubusercontent.com/opentargets/json\_schema/1.5.0/opentargets.json](https://raw.githubusercontent.com/opentargets/json_schema/1.5.0/opentargets.json) - \*should\* be backwards compatible, no evidence string changes needed
* API proxy
  * now baked into the REST API docker image
* New infrastructure associated with the 19.02 release
  * Because of the changes to the proxy above, \`proxy.opentargets.io\` should become \`platform-api.opentargets.io/proxy\`. The cause is that the Nginx proxy is included in the \`rest\_api\` docker image instead of being separate, which is easier for us to maintain and for partners to use.
  * Note: Eventually \(approx. 6 months\), \`proxy.opentargets.io\` will be decommissioned so anyone running pre-19.02 releases will need to update them.
* Pipeline Configuration
  * [https://github.com/opentargets/platform/issues/146](https://github.com/opentargets/platform/issues/146)
  * now configurable from two files - ops and data
  * data config file will be in public google bucket, can use for pipeline or download & customise
  * ops config can be on command line, or environment variable, or config file \(in decreasing priority\)
  * Example of data config: [https://storage.googleapis.com/open-targets-data-releases/19.02/input/mrtarget.data-2019-02-05.v3.yml](https://storage.googleapis.com/open-targets-data-releases/19.02/input/mrtarget.data-2019-02-05.v3.yml)
  * Example of ops config: [https://github.com/opentargets/data\_pipeline/blob/19.02.1/mrtarget.ops.yml](https://github.com/opentargets/data_pipeline/blob/19.02.1/mrtarget.ops.yml)
* Readme updates
  * including docker, make, config.
  * incorporates information from data\_release wiki, which is now deprecated [https://github.com/opentargets/platform/issues/259](https://github.com/opentargets/platform/issues/259)
* PyPI cleanup \(Python packaging infrastructure - where client is downloaded from\)
  * packages now have common "opentargets" prefix in the name \(except ontoma, working on it!\) [https://github.com/opentargets/platform/issues/233](https://github.com/opentargets/platform/issues/233)
* Pipeline technical improvements
  * better handling of --val threads [https://github.com/opentargets/platform/issues/350](https://github.com/opentargets/platform/issues/350)
  * better handling of --gen exceptions
  * better handling of remote resources
    * [https://github.com/opentargets/platform/issues/373](https://github.com/opentargets/platform/issues/373)
    * [https://github.com/opentargets/platform/issues/372](https://github.com/opentargets/platform/issues/372)
    * [https://github.com/opentargets/platform/issues/371](https://github.com/opentargets/platform/issues/371)
  * replace redis queue with pypeln in --hpa [https://github.com/opentargets/platform/issues/360](https://github.com/opentargets/platform/issues/360)
  * remove unused code \(PRs 426-432, 434-436\)
  * fix and improve elasticsearch bulk indexing
  * cleanup and improve ontology loading and lookup table construction ****

