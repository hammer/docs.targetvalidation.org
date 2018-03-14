## How do I add my own data to the platform?

> **Note**: If you are interested in injecting custom/private data, we are currently not supporting it, but are working towards it. It is feasible and it is indeed what our industry partners are doing to run their own customised installations. Contact us for more information. The process is briefly explained below:

While each data point that is included in the platform needs to conform to the JSON schema, the most basic requirement is that each data point contains a target \(in the form of an ENSGID number\) and a disease \(in the form of an ontology identifier, most often an EFO id\).



#### Transform your data into an array of JSON objects

Your data should be transformed in an array of JSON objects. The JSON database schema is \[publicly available\] \([https://github.com/opentargets/json\_schema](https://urldefense.proofpoint.com/v2/url?u=https-3A__github.com_opentargets_json-5Fschema&d=DwMFAw&c=n7UHtw8cUfEZZQ61ciL2BA&r=ZhzBE4adkrwWFCLwUz8sl2L08pOinkSBPT2-kXiY-Ls&m=kH1T4SDn11hFQ5Rsq4SaY01V95F6paxQ3cd3ENufcWQ&s=FoIdopSoY2bYDH5aCg3qH-ak6H3EbrikpyFf4cn05XY&e=)\)



#### Validate the data

To check the data you prepared can be processed by mrTarget, you can run our [validator](https://github.com/opentargets/validator) \([https://github.com/opentargets/validator](https://github.com/opentargets/validator) \) which will inform you of any inconsistencies in the data. 

After installation, the validator can be run: 

```
cat file.json | opentargets_validator --schema https://raw.githubusercontent.com/opentargets/json_schema/master/src/literature_curated.json

```



#### Run the pipeline \(mrTarget\)

Our pipeline parses and integrates multiple files containing _evidence_, discrete pieces of data linking target to diseases. It then aggregates them into _associations_ and ranks each target-to-disease connection according to the quality and quantity of each evidence. To add your data \(ie. a set of _evidences_\) to the platform, you need to add it to the pipeline processing.

> Note: We have not yet made our mrTarget pipeline open source. If you would like access in the meantime, please [contact us](mailto:support@targetvalidation.org).

Briefly - once you have access to the pipeline - you ought to

* fork it from github

* add the additional evidence datasource to the list of URLs contained in https://github.com/opentargets/data\_pipeline/blob/master/mrtarget/resources/evidences\_sources.txt
* Build a new docker container
* Start the evidence processing with `mrtarget --evs`



