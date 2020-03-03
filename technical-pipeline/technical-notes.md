---
description: >-
  This page summarises the key technical revisions made to platform code to
  improve and streamline the full stack code in line with major releases
  scheduled to incorporate new data and features.
---

# Technical notes

## 20.02

Open Targets Platform 20.02 was released on Monday 2 March 2020.

### Release synchronised with:

* EFO 3.14 \(January 2020\)
* Ensembl 98 \(September 2019\)

### **‌**Updated docker images:

* [quay.io/opentargets/mrtarget:20.02.1](https://quay.io/repository/opentargets/mrtarget?tag=20.02.1&tab=tags)
* [quay.io/opentargets/rest\_api:20.02.1](https://quay.io/repository/opentargets/rest_api?tag=20.02.1&tab=tags)
* [quay.io/opentargets/webapp:v3.16](https://quay.io/repository/opentargets/webapp?tag=v3.16&tab=tags)

### Pipeline configuration file:

* [https://storage.googleapis.com/open-targets-data-releases/20.02/input/mrtarget.data.20.02.yml](https://storage.googleapis.com/open-targets-data-releases/20.02/input/mrtarget.data.20.02.yml)

### **‌**Release **highlights:**

* Blog: [https://blog.opentargets.org/2020/03/02/open-targets-platform-release-20-02-is-out/](https://blog.opentargets.org/2020/03/02/open-targets-platform-release-20-02-is-out/)
* Release notes, including validated evidence string counts: [https://docs.targetvalidation.org/release-notes](https://docs.targetvalidation.org/release-notes)
* Release schedule and data submission details: [https://github.com/opentargets/data\_release/wiki/OT006-Data-Submission](https://github.com/opentargets/data_release/wiki/OT006-Data-Submission)

### **‌Technical release information:**

#### Infrastructure

* Update JSON schema to 1.6.4
* Fixed uploading of normal tissue file for platform-input-support scripts [\#776](https://github.com/opentargets/platform/issues/776)
* Fixed ES7 Docker image connection issue [\#736](https://github.com/opentargets/platform/issues/736)

#### **Data / Back-End**

* CHEMBL: updated evidence strings using CHEMBL26 data [\#835](https://github.com/opentargets/platform/issues/835), updated drug index [\#834](https://github.com/opentargets/platform/issues/834); ran adverse events pipeline with new drugs [\#833](https://github.com/opentargets/platform/issues/835)
* intOGen: updated evidence strings using latest intOGen release [\#813](https://github.com/opentargets/platform/issues/813)
* Changes in somatic mutation evidence normalization [\#811](https://github.com/opentargets/platform/issues/811)
* Updated CHEMBL-DrugBank ID mapping file [\#802](https://github.com/opentargets/platform/issues/802)
* Fixed GWAS evidence strings with a score of 0 [\#434](https://github.com/opentargets/platform/issues/434)
* GWAS evidences are now sourced from Open Targets Genetics portal instead of GWAS Catalog directly [\#815](https://github.com/opentargets/platform/issues/815)
* Fixed UniProt-Ensembl mapping issue [\#801](https://github.com/opentargets/platform/issues/801)

#### **Front-End**

* Fix to external links in RNA Expression data table on evidence page [\#812](https://github.com/opentargets/platform/issues/812)
* Added new TEP - MTHFR [\#458](https://github.com/opentargets/platform/issues/458)
* Updates to Somatic Mutation data table on evidence page [\#840](https://github.com/opentargets/platform/issues/840)
* Updates to Genetic Association data table on evidence page [\#816](https://github.com/opentargets/platform/issues/816)
* Association page facets updated to allow users to filter by Open Targets Genetics Portal evidence [\#849](https://github.com/opentargets/platform/issues/849)

## 19.11

19.11 was released on Thursday 28 November 2019

### Release synchronised with:

* EFO 3.11 \(October 2019\)
* Ensembl 98 \(September 2019\)

### Updated docker images:

* [quay.io/opentargets/mrtarget:19.11.4](https://quay.io/repository/opentargets/mrtarget?tag=19.11.4&tab=tags)
* [quay.io/opentargets/rest\_api:19.11.4](https://quay.io/repository/opentargets/rest_api?tag=19.11.4&tab=tags)
* [quay.io/opentargets/webapp:19.11.4](https://quay.io/repository/opentargets/webapp?tag=19.11.4&tab=tags)

### Pipeline configuration file:

* [https://storage.googleapis.com/open-targets-data-releases/19.11/input/mrtarget.data.19.11.yml](https://storage.googleapis.com/open-targets-data-releases/19.11/input/mrtarget.data.19.11.yml)

### Release highlights:

* Blog: [https://blog.opentargets.org/2019/11/28/open-targets-platform-release-19-11-is-out/](https://blog.opentargets.org/2019/11/28/open-targets-platform-release-19-11-is-out/)
* Release notes: [https://docs.targetvalidation.org/release-notes](https://docs.targetvalidation.org/release-notes)
* Data submission details: [https://github.com/opentargets/data\_release/wiki/OT006-Data-Submission](https://github.com/opentargets/data_release/wiki/OT006-Data-Submission) 

### Technical release information:

* Infrastructure:
  * Python 3 migration
    * Now running in Python 3: `data-pipeline` **\(Note: we expect the pipeline to continue to run with Python 2 but we will no longer support the pipeline in Python 2 as it has** [**reached its end-of-life**](https://www.python.org/doc/sunset-python-2/)**\)**
    * Running a mix of Python 2 and 3: `client`, `validator` and `ontologyutils` 
    * Still running in Python 2 only: Open Targets REST API and Open Targets LIterature coNcept Knowledgebase \(LINK\)
* Pipeline:
  * Migration to EFO3 **\(Note: the version of EFO3 present in the platform is a modified version of the ontology - otar\_slim - which is** [**available as part of EFO's official releases**](https://github.com/EBISPOT/efo/releases)**\)**
  * HPA step unicode error - [\#749](https://github.com/opentargets/platform/issues/749)
* REST API:
  * Add DrugBank ID - [\#612](https://github.com/opentargets/platform/issues/612)
  * Return clinical trial IDs in array - [\#686](https://github.com/opentargets/platform/issues/686)
  * Add canonical SMILES for a drug - [\#704](https://github.com/opentargets/platform/issues/704)
  * Add URLs to mechanism\_of\_action data - [\#687](https://github.com/opentargets/platform/issues/687) 
  * Add adverse events data - [\#739](https://github.com/opentargets/platform/issues/739)
  * Change to how EFO3 descriptions appear in API response - [\#756](https://github.com/opentargets/platform/issues/756)
* Front-end webapp:
  * Include new visualisation for adverse events data - [\#741](https://github.com/opentargets/platform/issues/741)
  * Display more details in drugs data tables - [\#730](https://github.com/opentargets/platform/issues/730) 
  * Fix bubbles and tree visualisations \(EFO3\) - [\#183](https://github.com/opentargets/platform/issues/183)
  * Fix disease classification visualisation \(EFO3\) - [\#457](https://github.com/opentargets/platform/issues/457)
  * Show DrugBank ID and link on drug profile page - [\#703](https://github.com/opentargets/platform/issues/703)
  * Bug fixes: [\#782](https://github.com/opentargets/platform/issues/782), [\#781](https://github.com/opentargets/platform/issues/781), [\#780](https://github.com/opentargets/platform/issues/780), [\#734](https://github.com/opentargets/platform/issues/734), [\#766](https://github.com/opentargets/platform/issues/766), [\#783](https://github.com/opentargets/platform/issues/783)
* Other:
  * LINK: review Python dependencies - [\#769](https://github.com/opentargets/platform/issues/769)
  * LINK: update dictionaries - [\#770](https://github.com/opentargets/platform/issues/770)
  * LINK: rerun pipeline with EFO3 - [\#750](https://github.com/opentargets/platform/issues/750)

## 19.09

### Release synchronised with:

EFO 2.106 \(March 2019 - final release of Version 2\)

Ensembl 97 \(July 2019\)

### Updated docker images:

* [quay.io/opentargets/mrtarget:19.09.5](https://quay.io/repository/opentargets/mrtarget?tag=19.09.5&tab=tags)
* [quay.io/opentargets/rest\_api:19.09.5](https://quay.io/repository/opentargets/rest_api?tag=19.09.5&tab=tags)
* [quay.io/opentargets/webapp:19.09.5](https://quay.io/repository/opentargets/webapp?tag=19.09.5&tab=tags)

### Pipeline configuration file:

* [https://storage.googleapis.com/open-targets-data-releases/19.09/input/mrtarget.data.19.09.yml](https://storage.googleapis.com/open-targets-data-releases/19.09/input/mrtarget.data.19.09.yml)

### Release highlights:

Blog: [http://blog.opentargets.org/2019/09/24/open-targets-platform-release-19-09-is-out/](http://blog.opentargets.org/2019/09/24/open-targets-platform-release-19-09-is-out/)

Release notes: [https://docs.targetvalidation.org/release-notes](https://docs.targetvalidation.org/release-notes)

### Technical release information:

* Infrastructure:
  * upgrade to elasticsearch 7.2 [https://github.com/opentargets/platform/issues/551](https://github.com/opentargets/platform/issues/551) in order to enable
    * removal of document types
    * handle changes to document total counts
    * add process-local caching
    * _**Note:  Update to ES V7.2 specifically, no further support for v5.6.**_
  * Platform input support improvements for QC of input files
* Pipeline:
  * remove redis [https://github.com/opentargets/data\_pipeline/pull/504](https://github.com/opentargets/data_pipeline/pull/504)
    * remove associated configuration and command line options
    * better parallelism
    * more maintainable code
    * potential small performance degradation
  * initiate work on python 3 migration [https://github.com/opentargets/platform/issues/459](https://github.com/opentargets/platform/issues/459)
  * remove ensembl stage [https://github.com/opentargets/platform/issues/321](https://github.com/opentargets/platform/issues/321)
  * remove uniprot stage [https://github.com/opentargets/platform/issues/322](https://github.com/opentargets/platform/issues/322)
  *  enable load of additional evidence to existing index [https://github.com/opentargets/platform/issues/632](https://github.com/opentargets/platform/issues/632)
* REST API:
  * Ensure compatibility with ES 7.2
  * Drug index improvements
  * Fix cache headers
* Webapp:
  * Drug summary page updates [https://github.com/opentargets/platform/issues/727](https://github.com/opentargets/platform/issues/727)
  * Minor updates to link-outs and downloads: 
    * [https://github.com/opentargets/platform/issues/662](https://github.com/opentargets/platform/issues/662)
    * [https://github.com/opentargets/platform/issues/220](https://github.com/opentargets/platform/issues/220)
    * [https://github.com/opentargets/platform/issues/657](https://github.com/opentargets/platform/issues/657)
  * Addition of new Target Enabling Packages
    * [https://github.com/opentargets/platform/issues/458](https://github.com/opentargets/platform/issues/458)

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

