# REST-API documentation

The [Open Targets REST-API](https://api.opentargets.io/v3/platform/docs/swagger-ui) is the alternative mode of access to the data available on the [Open Targets Platform](https://www.targetvalidation.org). It is language agnostic and it can be accessed from `https://api.opentargets.io/v3/platform`. 

Our current set of REST-API [endpoints](https://en.wikipedia.org/wiki/Web_API#Endpoints) can be divided in three groups:

* **Public** - Methods that serve the core set of our data e.g. associations and evidence. These methods are stable and unlikely to change.
* **Private** - Methods that serve other data in the Open Targets Platform, such as the [target profile page](https://docs.targetvalidation.org/getting-started/getting-started/target-profile) and [batch search](https://docs.targetvalidation.org/getting-started/batch-search). These methods may not be stable from one release to the next.
* **Utils** - Methods to get statistics on our data and to check if the server is alive.

To get the stats of our latest release, for example, you can use the following URL:

```text
https://api.opentargets.io/v3/platform/public/utils/stats
```

This endpoint will return the total number of targets and diseases, and the total numbers of associations and evidence strings per [data source](https://docs.targetvalidation.org/data-sources/data-sources) and data type.

The three methods listed above are available via a `GET` request, and by default will return the outputs in `JSON`.

{% hint style="info" %}
Alternative output formats, such `xml`, `csv` and `tab`, are also available for some of the methods e.g. [/association/filter](https://api.opentargets.io/v3/platform/docs/swagger-ui#/filter/getAssociationFilter) and [/search](https://api.opentargets.io/v3/platform/docs/swagger-ui#/search/getSearch).
{% endhint %}

For complex queries with large numbers of parameters, use  a `POST` request instead of `GET`. `POST` methods require a body encoded as `json`.

You can use the following tools with the REST-API endpoints:

* Command line \(e.g. CURL or HTTPie\)
* Open Targets [Python client](https://opentargets.readthedocs.io/en/stable/)
* Your own application and/or workflow

{% hint style="success" %}
We do provide a Python client but you can also access our REST-API with scripts in R or any other language.
{% endhint %}

{% hint style="info" %}
* Use any internet browser to test our REST API endpoints by pasting the URL in the location bar.
* Add a JSON plug-in to your internet browser for a human readable view of the results returned by the REST-API endpoint.
{% endhint %}

Check our blog for a series of [API posts](http://blog.opentargets.org/tag/api/) and our webinar [Take a rest of manual searches with the Open Targets API](https://www.youtube.com/watch?v=KQbfhwpeEvc&index=2&list=PLncWVtwSXtqb8PyL6-ENSCuqP7_4Aj5BE).

If you have questions on our REST-API, please [email us](mailto:support@targetvalidation.org) and will be happy to help.







