# REST-API endpoints

The [Open Targets REST-API](https://api.opentargets.io/v3/platform/docs/swagger-ui) is an alternative way to access the data available on the [Open Targets Platform](https://www.targetvalidation.org) in a programmatic manner. 

The current set of REST-API [endpoints](https://en.wikipedia.org/wiki/Web_API#Endpoints) can be divided in three groups:

* **Public** - Methods that serve the core set of our data e.g. associations and evidence. These methods are stable and unlikely to change.
* **Private** - Methods that serve other data in the Platform, such as the target profile page and batch search. These methods may change in between different releases.
* **Utils** - Methods to get statistics on our data and API version.

To get the stats of our latest release \(i.e. total number of targets and diseases, and the numbers of associations and evidence strings per data source and data type\), for example, you can use the following URL:

```text
https://api.opentargets.io/v3/platform/public/utils/stats
```

The three methods above are available via a `GET` request, and by default will return the outputs as `JSON`.

Alternative output formats, such `xml`, `csv` and `tab` , are also available for some of the methods.

If you have complex queries with large number of parameters, you should  
use a `POST` request instead of `GET`. `POST` methods require a body encoded as `json`.

You can use the following tools with the REST-API endpoints:

* Command line \(e.g. CURL or HTTPie\)
* Open Targets [Python client](https://opentargets.readthedocs.io/en/stable/)
* Your own application and workflow

{% hint style="info" %}
* Use any internet browser to test our REST API endpoints by pasting the URL in the location bar.
* Add a JSON plug-in to your internet browser for a human readable view of the results returned by the REST-API endpoint.
* Although we provide a Python client, you can access our REST-API with any other languages, including R.
{% endhint %}









