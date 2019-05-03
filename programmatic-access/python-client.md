# Python client

The python client for the Open Targets Platform REST API, `opentargets-py`, allows you to query the API automatically taking care of handling all the calls and returning data in a pythonic way.

The main advantages of using the client instead of querying the REST API directly are several fold. The python client:

* Includes wrappers for all public methods, with query validation
* Provides tools for the most common calls \(e.g. get data for a target gene symbol. You do not need to know its Ensembl Gene ID\)
* Supports automatic retrieval of paginated results with an iterator pattern
* Saves query results as JSON, CSV or Excel file
* Follows HTTP cache as set by the REST API
* Supports experimental HTTP2 for better performance \(beware the client library is in alpha\)

Head to our [Read the docs](%20https://opentargets.readthedocs.io/en/stable/) page for more details on:

* [installation](https://opentargets.readthedocs.io/en/stable/index.html#installation)
* [tutorial](https://opentargets.readthedocs.io/en/stable/tutorial.html)
* [code documentation](https://opentargets.readthedocs.io/en/stable/modules.html)
* and much more

{% hint style="warning" %}
This client is supported for Python 3.5.0 and more recent versions. It can also work on earlier versions such as python 2.7 on a best effort basis. 
{% endhint %}

If you have questions on the Open Targets python client, please [email us](mailto:support@targetvalidation.org).



