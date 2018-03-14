Our core stack is composed of three tiers:

* a client-side [web application](https://github.com/opentargets/webapp) that communicates with 
* a [Rest API](https://github.com/opentargets/rest_api) which retrieves and queries the data from 
* an ElasticSearch database; 

Each data-release we produce comes with an ElasticSearch snapshot \(ie. a _database_ _dump_\) to that can be used to create your own replica, using the `restore` ElasticSearch API.

The URL for the latest ES snapshot \(i.e. Dec 2017\) is:

`https://storage.googleapis.com/open-targets-data-releases/17.12/17.12_snapshot/`

\(please be aware of the size of the snapshot, which is roughly 100GB\).

The JSON database schema is \[publicly available\] \([https://github.com/opentargets/json\_schema](https://urldefense.proofpoint.com/v2/url?u=https-3A__github.com_opentargets_json-5Fschema&d=DwMFAw&c=n7UHtw8cUfEZZQ61ciL2BA&r=ZhzBE4adkrwWFCLwUz8sl2L08pOinkSBPT2-kXiY-Ls&m=kH1T4SDn11hFQ5Rsq4SaY01V95F6paxQ3cd3ENufcWQ&s=FoIdopSoY2bYDH5aCg3qH-ak6H3EbrikpyFf4cn05XY&e=)\)

**It is important to note** that this snapshot is different from the files availables on our Downloads page. Those evidence and association files are the product of a pre-processed export through our Rest API \([http://api.opentargets.io/v3/platform/docs](https://urldefense.proofpoint.com/v2/url?u=http-3A__api.opentargets.io_v3_platform_docs&d=DwMFAw&c=n7UHtw8cUfEZZQ61ciL2BA&r=ZhzBE4adkrwWFCLwUz8sl2L08pOinkSBPT2-kXiY-Ls&m=kH1T4SDn11hFQ5Rsq4SaY01V95F6paxQ3cd3ENufcWQ&s=WJWMFx9Gjum2gFZIOciZVlBA6cA5CTRIBZxPbxpsGDY&e=)\) using our python client \([https://github.com/opentargets/opentargets-py](https://urldefense.proofpoint.com/v2/url?u=https-3A__github.com_opentargets_opentargets-2Dpy&d=DwMFAw&c=n7UHtw8cUfEZZQ61ciL2BA&r=ZhzBE4adkrwWFCLwUz8sl2L08pOinkSBPT2-kXiY-Ls&m=kH1T4SDn11hFQ5Rsq4SaY01V95F6paxQ3cd3ENufcWQ&s=tG-jseMMiXHvfQf3DOh2b4TQO2KOCBYVdh4T6ktJKvE&e=)\). They cannot be used to restore our application. Although these files are not a database dump per se, they have been formatted and can serve as inputs for your in-house tools: each line represents a fully dumped \(serialised to a string\) JSON-object independent of each other

## How to restore using the public snapshot

### Pre-requisites:

* docker \(on mac osx you can install the [docker for mac](https://docs.docker.com/docker-for-mac/) app \)

Assuming you are following the official instructions and use [docker to run elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/docker.html), you can trigger the snapshot restore following these steps:

1\) Whitelist the url of our repo when you \`docker run\` by passing an environment variable:

```
docker run -d -p 9200:9200 -e 'discovery.type=single-node' -e 'xpack.security.enabled=false' –e 'repositories.url.allowed_urls=https://storage.googleapis.com/*' docker.elastic.co/elasticsearch/elasticsearch:5.6.8
```

If you get a "invalid reference format" error, doublecheck that the container tag has not changed by visiting the elasticsearch [docker container listings](https://www.docker.elastic.co/). It can also happen as a result of  copy/pasting the command from this documentation page. Try to re-type in your own shell.

You can check that ES is up and running by typing `curl localhost:9200` and you should get something that looks like:

```
{
    "cluster_name": "docker-cluster",
    "cluster_uuid": "Gt2Dsxh4StyV3YvdwBjx-Q",
    "name": "Z49nXRz",
    "tagline": "You Know, for Search",
    "version": {
        "build_date": "2018-02-16T16:46:30.010Z",
        "build_hash": "688ecce",
        "build_snapshot": false,
        "lucene_version": "6.6.1",
        "number": "5.6.8"
    }
}
```

More details on why you have to do specify `repositories.url.allowed_urls`  can be found in the official [elasticsearch documentation on read only URL repositories](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/modules-snapshots.html#_read_only_url_repository).

2\) then - again [following the documentation](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/modules-snapshots.html#_repositories) - you register the repo using the URL above:

```
curl -XPUT 'localhost:9200/_snapshot/ot_repo?verify=false&pretty' -H 'Content-Type: application/json' -d'
{
  "type": "url",
  "settings": {
    "url": "https://storage.googleapis.com/open-targets-data-releases/17.12/17.12_snapshot/"
}
}'
```

3\) when the last step completes succesfully, you can [trigger the snapshot restore:](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/modules-snapshots.html#_restore)

`curl -XPOST 'localhost:9200/_snapshot/ot_repo/<snapshot name> /_restore?pretty'`

you can find `<snapshot name>` by listing the snapshots in the repo, after step 2.

### Add your own data

If you are interested in injecting custom/private data, we are currently not supporting it, but are working towards it. It is feasible and it is indeed what our industry partners are doing to run their own customised installations. Contact us for more information.

