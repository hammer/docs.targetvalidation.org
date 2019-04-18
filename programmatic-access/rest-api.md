# REST API

The Open Targets Platform REST API allows language agnostic access to data available on the [Open Targets Platform](https://www.targetvalidation.org). The REST API can be accessed from:

`https://platform-api.opentargets.io/v3/platform`

Our current set of REST API [endpoints](https://en.wikipedia.org/wiki/Web_API#Endpoints) can be divided in three groups:

* **Public** - Methods that serve the core set of our data e.g. associations and evidence. These methods are stable and unlikely to change.
* **Private** - Methods that serve other data in the Open Targets Platform, such as the [target profile page](https://docs.targetvalidation.org/getting-started/getting-started/target-profile) and [batch search](https://docs.targetvalidation.org/getting-started/batch-search). These methods may not be stable from one release to the next. You should use these at your own risk.
* **Utils** - Methods to get statistics on our data and to check if the server is alive.

{% hint style="success" %}
Head to our [Swagger](https://api.opentargets.io/v3/platform/docs/swagger-ui) interface for a list of all available endpoints. You will also be able to test your queries in an interactive and easy manner.
{% endhint %}

To get the summary statistics of our latest release, for example, you will use the following URL:

```text
https://platform-api.opentargets.io/v3/platform/public/utils/stats
```

This `utils/stats` endpoint will return the total number of targets and diseases, and the total numbers of associations and evidence strings per [data source](https://docs.targetvalidation.org/data-sources/data-sources) and data type.

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
You can also access our REST-API with scripts in R or any other language.
{% endhint %}

Check our blog our webinar [Take a rest of manual searches with the Open Targets API](https://www.youtube.com/watch?v=KQbfhwpeEvc&index=2&list=PLncWVtwSXtqb8PyL6-ENSCuqP7_4Aj5BE) for an overview of the REST API and examples on some of API queries that serve the Open Targets Platform user interface.

{% embed url="https://www.youtube.com/watch?v=KQbfhwpeEvc&list=PLncWVtwSXtqb8PyL6-ENSCuqP7\_4Aj5BE&index=2" %}

{% hint style="danger" %}
Please note that at the time of the recording \(Dec 5th 2017\), the Open Targets REST API had a different URL. You should now use:

`https://platform-api.opentargets.io/v3/platform`
{% endhint %}

If you have questions on our REST API, please [email us](mailto:support@targetvalidation.org) and will be happy to help.







