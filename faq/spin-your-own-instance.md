Our core stack is a 3-tier one composed of a client-side [web application](https://github.com/opentargets/webapp) that communicates with a [Rest API](https://github.com/opentargets/rest_api) which retrieves and queries the data from an ElasticSearch instance; each data-release we produce comes with an ElasticSearch snapshot⁵ to be used as a valid copy to restore in your own instance. Thus, you will end up with a version of our public stack deployed on-premises.

If you are interested in injecting custom/private data, we are currently not supporting it, but are working towards it. It is feasible and it is indeed what our industry partners are doing to run their own customised installations. Contact us for more information.



