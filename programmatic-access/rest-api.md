# REST API



The Open Targets Platform REST API allows language agnostic access to data available on the Open Targets Platform. The REST API can be accessed from the following URL:

{% embed url="https://platform-api.opentargets.io/v3/platform" %}

The current set of REST API [endpoints](https://en.wikipedia.org/wiki/Web_API#Endpoints) can be divided in three methods:

* **Public** - Methods that serve the core set of our data e.g. associations and evidence. These methods are stable and unlikely to change.
* **Private** - Methods that serve other data in the Open Targets Platform, such as the [target profile page](https://docs.targetvalidation.org/getting-started/getting-started/target-profile) and [batch search](https://docs.targetvalidation.org/getting-started/batch-search). These methods may not be stable from one release to the next. You should use these at your own risk.
* **Utils** - Methods to get statistics on our data and to check if the server is alive.

By default these methods will return the outputs in `JSON`.

These are some of the [parameters](https://idratherbewriting.com/learnapidoc/docapis_doc_parameters.html) for the Open Targets Platform REST API :

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

Let's have a look at two examples below: `public/evidence/filter` and `public/search`. 

{% api-method method="get" host="https://platform-api.opentargets.io/v3/platform/public/evidence/filter?target=ENSG00000088832&datasource=chembl&size=15" path="" %}
{% api-method-summary %}
public/evidence/filter
{% endapi-method-summary %}

{% api-method-description %}
Retrieve the evidence used for a set of target-disease associations filtered by specific \(optional\) parameters.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}
datasource
{% endapi-method-parameter %}

{% api-method-parameter name="" type="string" required=false %}
target
{% endapi-method-parameter %}

{% api-method-parameter name="" type="integer" required=false %}
size
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

{% api-method method="get" host="https://platform-api.opentargets.io/v3/platform/public/search?q=dmd&size=23" path="" %}
{% api-method-summary %}
public/search
{% endapi-method-summary %}

{% api-method-description %}
Look up for a gene or disease identifier. This will replicate the search on the Open Targets Platform website.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}
size
{% endapi-method-parameter %}

{% api-method-parameter name="" type="string" required=true %}
q
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
took: 126,
data_version: "19.04",
query: {
highlight: true,
fields: null,
datastructure: "default",
format: "json",
size: 23
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
name_synonyms: [],
approved_name: "dystrophin",
hgnc_id: "HGNC:2928",
association_counts: {
total: 1251,
direct: 615
},
ensembl_gene_id: "ENSG00000198947",
symbol_synonyms: [],
biotype: "protein_coding",
full_name: "dystrophin",
type: "target",
id: "ENSG00000198947",
name: "DMD"
},
score: 2895.4158,
type: "search-object-target",
id: "ENSG00000198947",
highlight: {}
},
{},
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
Alternative output formats, such `xml`, `csv` and `tab`, may be also  available for some of the methods e.g. [/association/filter](https://api.opentargets.io/v3/platform/docs/swagger-ui#/filter/getAssociationFilter) and [/search](https://api.opentargets.io/v3/platform/docs/swagger-ui#/search/getSearch).
{% endhint %}

For complex queries with large numbers of parameters, use  a `POST` request instead of `GET`. `POST` methods require a body encoded as `json`.

You can use the following tools with the Open Targets Platform REST API endpoints:

* Command line \(e.g. CURL or HTTPie\)
* Your own application and/or workflow
* Open Targets Python client

{% hint style="success" %}
You can also access the Open Targets Platform REST-API with scripts in R. 
{% endhint %}

Check our webinar [Take a rest from manual searches with the Open Targets API](https://www.youtube.com/watch?v=KQbfhwpeEvc&index=2&list=PLncWVtwSXtqb8PyL6-ENSCuqP7_4Aj5BE) for an overview of the REST API and examples on some of the API queries that serve the Open Targets Platform user interface.

{% embed url="https://www.youtube.com/watch?v=KQbfhwpeEvc&list=PLncWVtwSXtqb8PyL6-ENSCuqP7\_4Aj5BE&index=2" %}

{% hint style="danger" %}
Please note that at the time of the recording \(Dec 5th 2017\), the Open Targets REST API had a different URL than the currently one in use. 

You should use:**`https://platform-api.opentargets.io/v3/platform`**
{% endhint %}

Check the [API tutorials](https://docs.targetvalidation.org/programmatic-access/api-tutorials) page for the most up-to-date use case examples or head to the [Open Targets Blog](https://blog.opentargets.org) for [Open Targets API Tutorial: Getting Started](http://blog.opentargets.org/2016/09/13/get-an-association-table-for-your-list-of-genes/) and [Get an association table for your list of genes](http://blog.opentargets.org/2016/09/13/get-an-association-table-for-your-list-of-genes/) tutorials.

{% hint style="warning" %}
Please note if you want to try out the tutorials available in the blog, you should amend the URL listed in there to the following:

**`https://platform-api.opentargets.io/v3/platform/`**
{% endhint %}

If you have questions on the Open Targets Platform REST API or need further help, please [email us](mailto:support@targetvalidation.org).

