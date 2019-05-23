# REST API

The Open Targets Platform REST API allows language agnostic access to data available on the Open Targets Platform. The REST API can be accessed from the following URL:

{% embed url="https://platform-api.opentargets.io/v3/platform" %}

The current set of REST API [endpoints](https://en.wikipedia.org/wiki/Web_API#Endpoints) can be divided in three groups:

* **Public** - Methods that serve the core set of our data e.g. associations and evidence. These methods are stable and unlikely to change.
* **Private** - Methods that serve other data in the Open Targets Platform, such as the [target profile page](https://docs.targetvalidation.org/getting-started/getting-started/target-profile) and [batch search](https://docs.targetvalidation.org/getting-started/batch-search). These methods may not be stable from one release to the next. You should use these at your own risk.
* **Utils** - Methods to get statistics on our data and to check if the server is alive.

Some of the [parameters](https://idratherbewriting.com/learnapidoc/docapis_doc_parameters.html) for the Open Targets Platform REST API are listed below:

* **target** - A target identifier listed as an Ensembl gene ID
* **disease** - A disease identifier listed as EFO, Orphanet, HP, or MONDO ID
* **datasource** - Data source used for target-disease associations
* **format** - By defaul the results are returned in JSON but you can retrieve the results as CSV, TAB and XML \(depending on the endpoint\)
* **direct** - It could be true \(direct associations\) or false \(indirect associations\)

   ****

{% hint style="info" %}
Not sure how to apply the `direct` parameter in the REST API call? Head to the blog post [Direct versus indirect evidence: should you care?](http://blog.opentargets.org/2017/04/25/direct-versus-indirect-evidence-should-you-care/)
{% endhint %}

We can break down a typical Open Targets Platform REST API call as follows:

|  |  |
| :--- | :--- |
| Server | https://platform-api.opentargets.io/v3/platform/ |
| Endpoint | e.g. public/association/filter |
| Parameters | e.g. ?target=ENSG00000163914&size=10000&fields=target.id&fields=disease.id |

{% hint style="success" %}
Head to our [Swagger](https://platform-api.opentargets.io/v3/platform/docs/swagger-ui) interface for a list of all available endpoints and parameters. You will also be able to test your queries in an interactive and easy manner before running your application/workflow.
{% endhint %}

{% api-method method="get" host="https://platform-api.opentargets.io/v3/platform/public/utils/stats" path="" %}
{% api-method-summary %}
Summary stats of the latest release
{% endapi-method-summary %}

{% api-method-description %}
Returns the number of associations and evidence strings per data source \(e.g. gwas\_catalog\) and data type \(e.g. genetic\_associations\) for the latest release.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
associations: {
datatypes: {
literature: {
total: 1708682,
datasources: {}
},
rna_expression: {},
somatic_mutation: {},
genetic_association: {
total: 468992,
datasources: {
gwas_catalog: {
total: 269000
},
uniprot_literature: {
total: 39556
},
eva: {
total: 64113
},
gene2phenotype: {
total: 20944
},
genomics_england: {
total: 46024
},
uniprot: {
total: 40182
},
phewas_catalog: {
total: 136310
}
}
},
known_drug: {
total: 115016,
datasources: {
chembl: {
total: 115016
}
}
},
animal_model: {
total: 1114830,
datasources: {
phenodigm: {
total: 1114830
}
}
},
affected_pathway: {
total: 144716,
datasources: {
sysbio: {
total: 1525
},
reactome: {
total: 7669
},
crispr: {
total: 9175
},
progeny: {
total: 1288
},
slapenrich: {
total: 128548
}
}
}
},
total: 3303824
},
data_version: "19.04",
evidencestrings: {
datatypes: {
literature: {
total: 5438280,
datasources: {
europepmc: {
total: 5438280
}
}
},
rna_expression: {
total: 381141,
datasources: {
expression_atlas: {
total: 381141
}
}
},
somatic_mutation: {
total: 69704,
datasources: {
cancer_gene_census: {
total: 59992
},
uniprot_somatic: {
total: 284
},
eva_somatic: {
total: 7057
},
intogen: {
total: 2371
}
}
},
genetic_association: {
total: 348090,
datasources: {
gwas_catalog: {
total: 157008
},
uniprot_literature: {
total: 4567
},
eva: {
total: 89636
},
gene2phenotype: {
total: 1589
},
genomics_england: {
total: 10533
},
uniprot: {
total: 28743
},
phewas_catalog: {
total: 56014
}
}
},
known_drug: {
total: 384783,
datasources: {
chembl: {
total: 384783
}
}
},
animal_model: {
total: 500462,
datasources: {
phenodigm: {
total: 500462
}
}
},
affected_pathway: {
total: 87015,
datasources: {
sysbio: {
total: 408
},
reactome: {
total: 10083
},
crispr: {
total: 1641
},
progeny: {
total: 308
},
slapenrich: {
total: 74575
}
}
}
},
total: 7209475
},
targets: {
total: 28501
},
diseases: {
total: 10419
}
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

This `utils/stats` endpoint will also return the total number of targets and diseases, and data type.

The three methods listed above \(**Public**, **Private** and **Utils**\) are available via a `GET` request, and by default will return the outputs in `JSON`.

{% hint style="info" %}
Alternative output formats, such `xml`, `csv` and `tab`, are also available for some of the methods e.g. [/association/filter](https://api.opentargets.io/v3/platform/docs/swagger-ui#/filter/getAssociationFilter) and [/search](https://api.opentargets.io/v3/platform/docs/swagger-ui#/search/getSearch).
{% endhint %}

For complex queries with large numbers of parameters, use  a `POST` request instead of `GET`. `POST` methods require a body encoded as `json`.

You can use the following tools with the Open Targets Platform REST API endpoints:

* Command line \(e.g. CURL or HTTPie\)
* Your own application and/or workflow
* Open Targets Python client

{% hint style="success" %}
You can also access the Open Targets Platform REST-API with scripts in R. 
{% endhint %}

Check our webinar [Take a rest of manual searches with the Open Targets API](https://www.youtube.com/watch?v=KQbfhwpeEvc&index=2&list=PLncWVtwSXtqb8PyL6-ENSCuqP7_4Aj5BE) for an overview of the REST API and examples on some of the API queries that serve the Open Targets Platform user interface.

{% embed url="https://www.youtube.com/watch?v=KQbfhwpeEvc&list=PLncWVtwSXtqb8PyL6-ENSCuqP7\_4Aj5BE&index=2" %}

{% hint style="danger" %}
Please note that at the time of the recording \(Dec 5th 2017\), the Open Targets REST API had a different URL than the currently one in use. 

You should use:**`https://platform-api.opentargets.io/v3/platform`**
{% endhint %}

Check the [API tutorials](https://app.gitbook.com/@opentargets/s/docs/~/edit/drafts/-LeTHkA8HTdP8dQFx9Ig/programmatic-access/api-tutorials) page for the most up-to-date use case examples or head to the [Open Targets Blog](https://blog.opentargets.org) for [Open Targets API Tutorial: Getting Started](http://blog.opentargets.org/2016/09/13/get-an-association-table-for-your-list-of-genes/) and [Get an association table for your list of genes](http://blog.opentargets.org/2016/09/13/get-an-association-table-for-your-list-of-genes/) tutorials.

{% hint style="warning" %}
Please note if you want to try out the tutorials available in the blog, you should amend the URL listed in there to the following:

**`https://platform-api.opentargets.io/v3/platform/`**
{% endhint %}

If you have questions on the Open Targets Platform REST API or need further help, please [email us](mailto:support@targetvalidation.org).

