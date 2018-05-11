# Data download

Yes, you can download our data as compressed JSON files. These [file dumps are available](http://www.targetvalidation.org/downloads/data) for the target-disease association objects and the evidence objects, the latter used to calculate each association. Both association and evidence objects are also available programmatically via our API \(check our [API documentation](http://api.opentargets.io/v3/platform/docs)\).

Both files, evidence and association, cannot be used to restore the application. Although they are the result of a data dump, they are not in the sense of a proper database dump. These files are the product of a preprocessed export through our [Rest API](http://api.opentargets.io/v3/platform/docs) using our [python client](https://github.com/opentargets/opentargets-py). Nevertheless, the dump files are meticulously formatted to serve as inputs for your in-house tools; each line represents a fully dumped \(serialised to a string\) JSON-object independent of each other.

