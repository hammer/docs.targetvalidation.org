# REST API

The Open Targets Platform REST API allows language agnostic access to data available on the Open Targets Platform. It can be accessed from the following URL:

{% embed url="https://platform-api.opentargets.io/v3/platform" %}

The Open Targets Platform REST API [endpoints](https://en.wikipedia.org/wiki/Web_API#Endpoints) can be divided in three methods:

* **Public** - Methods that serve the core set of data e.g. associations and evidence. These methods are stable and unlikely to change.
* **Private** - Methods that serve other data in the Open Targets Platform, such as the [target profile page](https://docs.targetvalidation.org/getting-started/getting-started/target-profile) and [batch search](https://docs.targetvalidation.org/getting-started/batch-search). These methods may not be stable from one release to the next. You should use these at your own risk.
* **Utils** - Methods to get statistics on our data and to check if the server is alive.

These are some of the [parameters](https://idratherbewriting.com/learnapidoc/docapis_doc_parameters.html) for the Open Targets Platform REST API :

* **target** - A target identifier listed as an Ensembl gene ID
* **disease** - A disease identifier listed as EFO, Orphanet, HP, or MONDO ID
* **datasource** - Data source used for target-disease associations
* **datatype** - Data type used for target-disease associations
* **format** - By default the results are returned in JSON but you can retrieve the results as CSV, TAB and XML \(depending on the endpoint\)
* **scorevalue\_min** - It can be used to filter \(associations ou evidence\) by a minimum score value. The default is 0. Scores above 0.2 is a good trade-off to filter lower quality data points
* **direct** - It could be _true_ \(direct associations\) or _false_ \(indirect associations\)

{% hint style="info" %}
Not sure how to apply the `direct` parameter in the REST API call? Check [Direct versus indirect evidence: should you care?](http://blog.opentargets.org/2017/04/25/direct-versus-indirect-evidence-should-you-care/) blog post for more information.
{% endhint %}

A typical Open Targets Platform REST API call can be broken down as follows:

|  |  |
| :--- | :--- |
| Server | https://platform-api.opentargets.io/v3/platform/ |
| Endpoint | e.g. public/association/filter |
| Parameters | e.g. ?target=ENSG00000163914&size=10000&fields=target.id&fields=disease.id |

{% hint style="success" %}
Head to the [Swagger](https://platform-api.opentargets.io/v3/platform/docs/swagger-ui) interface for a list of all available endpoints,  parameters and filters.

You will also be able to test your queries in an interactive and easy manner before running your application/workflow.
{% endhint %}

Let's have a look at a few examples of endpoints, such as`public/search`, `public/association` and `public/evidence/filter`:

## The search endpoint

It looks up for the Ensembl gene ID or the disease ID \(EFO, HP, Orphanet, MONDO\) using a free text search. It should be used to identify the best match for a disease or target of interest, rather than gathering a specific set of evidence.

Searching for DMD, for example, will return its Ensembl gene ID, ENSG00000198947, in addition to other data, such as names and IDs of orthologues, association counts, approved name and much more. You need these stable IDs to query the REST API using the remaining endpoints.

{% api-method method="get" host="https://platform-api.opentargets.io/v3/platform/public/search?q=dmd" path=" " %}
{% api-method-summary %}
public/search
{% endapi-method-summary %}

{% api-method-description %}
It allows you to look for gene or diseases of interest using a free text search, replicating the functionality of the search box in the Open Targets Platform website. It should be used to identify the best match for a disease or target, rather than gathering a specific set of evidence.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}
size
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
from: 0,
took: 103,
data_version: "19.09",
query: {
highlight: true,
fields: null,
datastructure: "default",
format: "json",
size: 10
},
total: 23,
data: [
{
data: {
ortholog: {},
top_associations: {},
approved_symbol: "DMD",
description: "Anchors the extracellular matrix to the cytoskeleton via F-actin. Ligand for dystroglycan. Component of the dystrophin-associated glycoprotein complex which accumulates at the neuromuscular junction (NMJ) and at a variety of synapses in the peripheral and central nervous systems and has a structural function in stabilizing the sarcolemma. Also implicated in signaling events and synaptic transmission.",
uniprot_accessions: [],
drugs: {},
gene_family_description: "",
name_synonyms: [
"muscular dystrophy, Duchenne and Becker types",
"Dystrophin"
],
approved_name: "dystrophin",
hgnc_id: "HGNC:2928",
association_counts: {
total: 1281,
direct: 635
},
ensembl_gene_id: "ENSG00000198947",
symbol_synonyms: [
"BMD",
"DXS142",
"DXS164",
"DXS206",
"DXS230",
"DXS239",
"DXS268",
"DXS269",
"DXS270",
"DXS272"
],
biotype: "protein_coding",
full_name: "dystrophin",
type: "target",
id: "ENSG00000198947",
name: "DMD"
},
score: 2752.9067,
type: "search-object-target",
id: "ENSG00000198947",
highlight: {}
},
{},
{},
{},
{},
{},
{},
{},
{},
{}
],
size: 10
}- -- 
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## The association endpoint

It retrieves the [association scores](https://docs.targetvalidation.org/getting-started/scoring) for an association between any target and disease, replicating the results seen on the website when viewing the associations for a target \(e.g. [NOD2](https://www.targetvalidation.org/target/ENSG00000167207/associations)\) or for a disease \(e.g. [Noonan syndrome](https://www.targetvalidation.org/disease/Orphanet_648/associations)\).

You can retrieve the association either by an ID \(in the format of `TARGET_ID-DISEASE_ID)` or you can also use the `association/filter` endpoint instead.

In addition to the association scores, you will also get the data and summary on each evidence type included in the calculation of the score.

{% api-method method="get" host="https://platform-api.opentargets.io/v3/platform/public/association?id=ENSG00000073756-EFO\_0003767    " path="" %}
{% api-method-summary %}
public/association
{% endapi-method-summary %}

{% api-method-description %}
Get the association scores for one target-disease using the association ID, in the format of \`Ensembl Gene ID-disease ID\` e.g. \`ENSG00000073756-EFO\_0003767\`.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="" type="string" required=true %}
ID
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
from: 0,
took: 2,
data_version: "19.09",
query: { },
total: 1,
data: [
{
target: {},
association_score: {
datatypes: {
literature: 0.15637867953616,
rna_expression: 0.011508835806466024,
somatic_mutation: 0,
genetic_association: 0,
known_drug: 1,
animal_model: 0.27356111111111114,
affected_pathway: 0
},
overall: 1,
datasources: {
slapenrich: 0,
sysbio: 0,
expression_atlas: 0.011508835806466024,
gene2phenotype: 0,
progeny: 0,
chembl: 1,
uniprot_literature: 0,
phenodigm: 0.27356111111111114,
eva: 0,
europepmc: 0.15637867953616,
gwas_catalog: 0,
uniprot_somatic: 0,
genomics_england: 0,
postgap: 0,
uniprot: 0,
crispr: 0,
cancer_gene_census: 0,
reactome: 0,
intogen: 0,
eva_somatic: 0,
phewas_catalog: 0
}
},
max: {},
sum: {},
is_direct: true,
private: {},
disease: {},
evidence_count: {},
id: "ENSG00000073756-EFO_0003767"
}
],
size: 1
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://platform-api.opentargets.io/v3/platform/public/association/filter?target=ENSG00000073756&datasource=chembl" path="" %}
{% api-method-summary %}
public/association/filter
{% endapi-method-summary %}

{% api-method-description %}
It allows for more complex and flexible queries to get association scores and objects \(e.g. filter the results by score and associated pathways, sort the results\).
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="direct" type="string" required=false %}
true
{% endapi-method-parameter %}

{% api-method-parameter name="datasource" type="string" required=false %}
gene2phenotype
{% endapi-method-parameter %}

{% api-method-parameter name="datatype" type="string" required=false %}
genetic\_association
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## The evidence endpoint, with filters for specific data

It retrieves the evidence used for an association and allow for specific filters to be added, so that you can restrict the results by data type, data source, or limit the results to targets that are part of a given pathway. You can also specify minimum and maximum scores, as well as the format of the results \(e.g. `csv` or `xml`\).

{% api-method method="get" host="https://platform-api.opentargets.io/v3/platform/public/evidence/filter?target=ENSG00000088832&datasource=chembl&size=15" path="" %}
{% api-method-summary %}
public/evidence/filter
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="datatype" type="string" required=false %}
genetic\_association, somatic\_mutation, known\_drug, etc.
{% endapi-method-parameter %}

{% api-method-parameter name="target" type="string" required=false %}
target ID as Ensembl gene ID
{% endapi-method-parameter %}

{% api-method-parameter name="size" type="integer" required=false %}
number of results returned
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text
{
from: 0,
took: 2,
next: [
1,
"ebf0bce9cc8b956ce1d2d0200756431e"
],
data_version: "19.04",
query: {},
total: 1474,
data: [],
size: 15
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
Alternative output formats, such `xml`, `csv` and `tab`, may be also  available for some of the methods e.g. [/association/filter](https://api.opentargets.io/v3/platform/docs/swagger-ui#/filter/getAssociationFilter) and [/search](https://api.opentargets.io/v3/platform/docs/swagger-ui#/search/getSearch).
{% endhint %}

{% hint style="success" %}
Note that multiple genes and diseases can be specified in the same request by using the `&` e.g.

[https://platform-api.opentargets.io/v3/platform/public/association/filter?target=ENSG00000100652&target=ENSG00000125255&target=ENSG00000126903&target=ENSG00000137571&target=ENSG00000205359](https://platform-api.opentargets.io/v3/platform/public/association/filter?target=ENSG00000100652&target=ENSG00000125255&target=ENSG00000126903&target=ENSG00000137571&target=ENSG00000205359)
{% endhint %}

For complex queries with large numbers of parameters, use  a `POST` request instead of `GET`. `POST` methods require a body \(or payload\) encoded as `json`.

You can also output these results with the following tools:

* Command line \(e.g. CURL, WGET or HTTPie\)
* Your own application and/or workflow
* Open Targets [Python client](https://docs.targetvalidation.org/programmatic-access/python-client)

{% hint style="success" %}
You can also access the Open Targets Platform REST-API with scripts in R. 
{% endhint %}

Check our webinar [Take a rest from manual searches with the Open Targets API](https://www.youtube.com/watch?v=KQbfhwpeEvc&index=2&list=PLncWVtwSXtqb8PyL6-ENSCuqP7_4Aj5BE) for an overview of the REST API and examples on some of the API queries that serve the Open Targets Platform user interface.

{% embed url="https://www.youtube.com/watch?v=KQbfhwpeEvc&list=PLncWVtwSXtqb8PyL6-ENSCuqP7\_4Aj5BE&index=2" %}

{% hint style="danger" %}
Please note that at the time of the recording \(Dec 5th 2017\), the Open Targets REST API had a different URL than the currently one in use. 

You should now use:**`https://platform-api.opentargets.io/v3/platform`**
{% endhint %}

Head to the [API tutorials](https://docs.targetvalidation.org/programmatic-access/api-tutorials) page a few use case examples on using the Open Targets Platform REST API and [email us](mailto:support@targetvalidation.org) if you have questions or want to discuss other use cases.

