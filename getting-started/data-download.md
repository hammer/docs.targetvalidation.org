# Data download

You can download the target-disease associations and the evidence used for the associations from the [Data Download](https://www.targetvalidation.org/downloads/data) page. 

This data is available as compressed JSON files and can also be obtained programmatically using the `/public/association` and `/public/evidence` REST API methods. Check [Open Targets Platform REST API](https://docs.targetvalidation.org/tutorials/rest-api) help page for more details.

{% hint style="warning" %}
Both association and evidence files available for download cannot be used to restore the application as they are not a database dump. These files are the product of a preprocessed export through the Open Targets Platform [REST API](https://docs.targetvalidation.org/programmatic-access/rest-api) using the Open Targets [Python client](https://docs.targetvalidation.org/programmatic-access/python-client). 

These dump files are meticulously formatted to serve as inputs for your in-house tools: each line represents a fully dumped \(serialised to a string\) JSON-object independent of each other.
{% endhint %}

Head to the FAQs section if you [want to spin your own instance of the Platform](https://docs.targetvalidation.org/faq/spin-your-own-instance).

