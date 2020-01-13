# Data download

You can download the target-disease associations and the evidence used for the associations from the [Data Download](https://www.targetvalidation.org/downloads/data) page. 

This data is available as compressed JSON files. These files are meticulously formatted to serve as inputs for in-house tools: each line represents a fully dumped \(serialised to a string\) JSON-object, which are independent of each other.

{% hint style="warning" %}
The association and evidence files available for download cannot be used to restore the application as they are not a database dump. These files are the product of a preprocessed export through the Open Targets Platform [REST API](https://docs.targetvalidation.org/programmatic-access/rest-api) using the Open Targets [Python client](https://docs.targetvalidation.org/programmatic-access/python-client), for example using the `/public/association` and `/public/evidence` endpoints. 
{% endhint %}

Head to the Open Targets Platform FAQs, if you [want to spin your own instance of the Platform](https://docs.targetvalidation.org/faq/spin-your-own-instance).





