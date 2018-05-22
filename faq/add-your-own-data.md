# Can I add private data?

> **Note**: If you are interested in injecting custom/private data, we currently support this to our industry partners only. We are working towards supporting this for users outside the Open Targets Partnership. At any rate, the local installation process is summarised below:

While each data point that is included in the Platform needs to conform to our JSON schema, the most basic requirement is that each data point contains a target \(in the form of an Ensembl gene ID\) and a disease \(in the form of an ontology identifier, most often an EFO ID\).

## Transform your data into an array of JSON objects

You need to transform your data in an array of JSON objects. The JSON database schema is publicly available on our [GitHub](https://github.com/opentargets/json_schema).

Each object requires mapping to an ENS gene ID and an EFO ID \(or HP terms, in case the EFO term is missing\). We have a light wrapper called [OnToma](https://github.com/opentargets/OnToma\) to facilitate this mapping process.

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

## Run the pipeline \(mrTarget\)

Our pipeline parses and integrates multiple files containing _evidence_, discrete pieces of data linking target to diseases. It then aggregates them into _associations_ and ranks each target-disease connection according to the quality and quantity of each evidence. To inject your own data \(i.e. a set of _evidence_\) to the Open Targets Platform, you need to add it to the pipeline processing.

> Note: We are currently making our mrTarget pipeline open source. In the meantime if you want to access it, please [contact us](mailto:support@targetvalidation.org).

Briefly - once you have access to the pipeline - you ought to

* Fork it from GitHub
* Add the additional evidence to the list of Open Targets data sources
* Build a new docker container
* Start the evidence processing with `mrtarget --evs`

