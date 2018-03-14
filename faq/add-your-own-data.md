## How do I add my own data to the platform?

If you are interested in injecting custom/private data, we are currently not supporting it, but are working towards it. It is feasible and it is indeed what our industry partners are doing to run their own customised installations. Contact us for more information.

The JSON database schema is \[publicly available\] \([https://github.com/opentargets/json\_schema](https://urldefense.proofpoint.com/v2/url?u=https-3A__github.com_opentargets_json-5Fschema&d=DwMFAw&c=n7UHtw8cUfEZZQ61ciL2BA&r=ZhzBE4adkrwWFCLwUz8sl2L08pOinkSBPT2-kXiY-Ls&m=kH1T4SDn11hFQ5Rsq4SaY01V95F6paxQ3cd3ENufcWQ&s=FoIdopSoY2bYDH5aCg3qH-ak6H3EbrikpyFf4cn05XY&e=)\)





While each data point that is included in the platform needs to conform to the JSON schema, the most basic requirement is that each data point contains a target \(in the form of an ENSGID number\) and a disease \(in the form of an ontology identifier, most often an EFO id\). 



To check the data you prepared can be processed by mrTarget, you can run our [validator](https://github.com/opentargets/validator) \(https://github.com/opentargets/validator \) which will inform you of any inconsistencies in the data, which will impede its inclusion.

