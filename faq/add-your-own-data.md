# Can I add private data?

The Open Targets Platform integrates genetics, genomics and chemical information from publicly available data sources, but you can also add your own private data if [you spin your own instance of the Platform](https://docs.targetvalidation.org/faq/spin-your-own-instance).

The  pre-requisites when considering adding your private data are as follows. 

You data should:

* contain a target identified by Ensembl gene ID
* contain a disease or phenotype identified by an ontology term e.g. EFO, HP, Orphanet, MONDO.
* conform to our JSON schema

{% hint style="success" %}
Looking for step-by-step instructions on how to add a new data source to the Open Targets Platform? Head to Open Targets Blog for a series of posts by [Glenn Proctor](http://blog.opentargets.org/author/glennproctor/).
{% endhint %}

## Transform your data into an array of JSON objects

You need to transform your data in an array of JSON objects. The JSON database schema is publicly available on [GitHub](https://github.com/opentargets/json_schema).

Each object requires mapping to an Ensembl gene ID and an EFO ID \(or HP terms, in case the EFO term is missing\). We have a light wrapper called [OnToma](https://github.com/opentargets/OnToma\) to facilitate this mapping process.

Once the conversion is done, you will have an array containing a JSON object. For instance, our PheWAS evidence will look something like this:

```text
[{"target": {..  "http://identifiers.org/ensembl/ENSG00000130204", }, "sourceID": "phewas_catalog", 
    "variant": {"type": "snp single", "id": "http://identifiers.org/dbsnp/rs2075650"}, 
    "disease": {"id": "EFO:0000249"}, 
    "unique_association_fields": {..}, 
    "evidence": {... , "value": "5.237e-28"}, 
     "type": "genetic_association", "resource_score": {...}}
{"target": { ... } disease: {...} ... }
{"target": { ...}, ...}
...
]
```

## Validate the data

Before processing your data, you should run Open Targets [validator](https://github.com/opentargets/validator) to check for any inconsistencies in your data.

After installation, the validator can be run as it follows:

```text
cat file.json | opentargets_validator --schema https://raw.githubusercontent.com/opentargets/json_schema/1.6.0/opentargets.json
```

## Run the Open Targets Platform data pipeline \(mrTarget\)

The Open Targets Platform pipeline parses and integrates multiple files containing **evidence**, discrete pieces of data linking targets to diseases. It then aggregates them into **associations** and ranks each target-disease connections according to the quality and quantity of each evidence. To inject your own data \(i.e. a set of **evidence**\) to the Open Targets Platform, you need to add it to the pipeline processing.

{% hint style="success" %}
The data pipeline for the Open Targets Platform is open source. The code for its processing can be found on [GitHub. ](https://github.com/opentargets/data_pipeline)
{% endhint %}

Briefly - once you have access to the pipeline - you ought to:

* Fork it from GitHub
* Add the additional evidence to the list of Open Targets data sources
* Build a new docker container
* Start the evidence processing with `mrtarget --evs`

{% hint style="warning" %}
We currently support private data injection to our industry partners only. If you want to discuss this further, please [email us](mailto:support@targetvalidation.org).
{% endhint %}

## 

