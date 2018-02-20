Our core stack is a 3-tier one composed of:

* a client-side [web application](https://github.com/opentargets/webapp) that communicates with 
* a [Rest API](https://github.com/opentargets/rest_api) which retrieves and queries the data from 
* an ElasticSearch instance; 

Each data-release we produce comes with an ElasticSearch snapshot to be used as a valid copy to restore in your own instance.

The link to the latest ES snapshot \(i.e. Dec 2017\):

[https://console.cloud.google.com/storage/browser/open-targets-data-releases/17.12/17.12\_snapshot/](https://console.cloud.google.com/storage/browser/open-targets-data-releases/17.12/17.12_snapshot/?project=open-targets-prod&organizationId=817248562955)

\(please be aware of the size of the snapshot, which is roughly 100GB\).

The JSON database schema is \[publicly available\] \([https://github.com/opentargets/json\_schema](https://urldefense.proofpoint.com/v2/url?u=https-3A__github.com_opentargets_json-5Fschema&d=DwMFAw&c=n7UHtw8cUfEZZQ61ciL2BA&r=ZhzBE4adkrwWFCLwUz8sl2L08pOinkSBPT2-kXiY-Ls&m=kH1T4SDn11hFQ5Rsq4SaY01V95F6paxQ3cd3ENufcWQ&s=FoIdopSoY2bYDH5aCg3qH-ak6H3EbrikpyFf4cn05XY&e=)\)

**Note** this snapshot is different from the files availables on our Downloads page. Those evidence and association files are the product of a pre-processed export through our Rest API \([http://api.opentargets.io/v3/platform/docs](https://urldefense.proofpoint.com/v2/url?u=http-3A__api.opentargets.io_v3_platform_docs&d=DwMFAw&c=n7UHtw8cUfEZZQ61ciL2BA&r=ZhzBE4adkrwWFCLwUz8sl2L08pOinkSBPT2-kXiY-Ls&m=kH1T4SDn11hFQ5Rsq4SaY01V95F6paxQ3cd3ENufcWQ&s=WJWMFx9Gjum2gFZIOciZVlBA6cA5CTRIBZxPbxpsGDY&e=)\) using our python client \([https://github.com/opentargets/opentargets-py](https://urldefense.proofpoint.com/v2/url?u=https-3A__github.com_opentargets_opentargets-2Dpy&d=DwMFAw&c=n7UHtw8cUfEZZQ61ciL2BA&r=ZhzBE4adkrwWFCLwUz8sl2L08pOinkSBPT2-kXiY-Ls&m=kH1T4SDn11hFQ5Rsq4SaY01V95F6paxQ3cd3ENufcWQ&s=tG-jseMMiXHvfQf3DOh2b4TQO2KOCBYVdh4T6ktJKvE&e=)\). They cannot be used to restore our application I'm afraid to say. Although these files are not a database dump per se, they have been formatted and can serve as inputs for your in-house tools: each line represents a fully dumped \(serialised to a string\) JSON-object independent of each other

### Add your own data

If you are interested in injecting custom/private data, we are currently not supporting it, but are working towards it. It is feasible and it is indeed what our industry partners are doing to run their own customised installations. Contact us for more information.

