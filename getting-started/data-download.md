# Data download

You can download the target-disease associations and the evidence used for the associations from our [Data Download](https://www.targetvalidation.org/downloads/data) page. 

This data is available as compressed JSON files and can also be obtained programmatically using the `/public/associations` and `/public/evidence` REST API methods. Check [Open Targets Platform REST API](https://docs.targetvalidation.org/tutorials/rest-api) help page for more details.

{% tabs %}
{% tab title="Note" %}
Both association and evidence files cannot be used to restore the application as they are not a database dump. These files are the product of a preprocessed export through the Open Targets REST API using [opentargets-py](https://github.com/opentargets/opentargets-py), our python client. 

These dump files are meticulously formatted to serve as inputs for your in-house tools: each line represents a fully dumped \(serialised to a string\) JSON-object independent of each other.
{% endtab %}
{% endtabs %}



