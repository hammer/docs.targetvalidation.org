# Can I add private data?



The Open Targets Platform integrates multiomics and chemical information from public available data sources.

You can inject your own custom or private data following the summary below. The  pre-requisites are as follows:

* data contains a target identified by Ensembl gene ID
* data contains a disease or phenotype identified by an ontology term e.g. EFO, HP, Orphanet
* data should conform to our JSON schema

{% hint style="warning" %}
We currently support private data injection to our industry partners only. If you want to discuss this further, please [email us](mailto:support@targetvalidation.org).
{% endhint %}

## Transform your data into an array of JSON objects

You need to transform your data in an array of JSON objects. The JSON database schema is publicly available on our [GitHub](https://github.com/opentargets/json_schema).

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

Before processing your data, you should run our [validator](https://github.com/opentargets/validator) to check for any inconsistencies in your data.

After installation, the validator can be run as it follows:

```text
cat file.json | opentargets_validator --schema https://raw.githubusercontent.com/opentargets/json_schema/master/src/literature_curated.json
```

## Run the Open Targets Platform data pipeline \(mrTarget\)

Our pipeline parses and integrates multiple files containing _evidence_, discrete pieces of data linking target to diseases. It then aggregates them into _associations_ and ranks each target-disease connection according to the quality and quantity of each evidence. To inject your own data \(i.e. a set of _evidence_\) to the Open Targets Platform, you need to add it to the pipeline processing.

{% hint style="success" %}
The data pipeline for the Open Targets Platform is open source. The code for its processing can be found on [GitHub. ](https://github.com/opentargets/data_pipeline)
{% endhint %}

Briefly - once you have access to the pipeline - you ought to:

* Fork it from GitHub
* Add the additional evidence to the list of Open Targets data sources
* Build a new docker container
* Start the evidence processing with `mrtarget --evs`

