Our core stack is composed of three tiers:

1. a client-side [web application](https://github.com/opentargets/webapp) \([https://github.com/opentargets/webapp\](https://github.com/opentargets/webapp%29\) that communicates with 
2. a [Rest API](https://github.com/opentargets/rest_api) \([https://github.com/opentargets/rest\_api\](https://github.com/opentargets/rest_api%29\) which retrieves and queries the data from 
3. an ElasticSearch database; 

Each data-release we produce comes with an ElasticSearch snapshot \(ie. a _database_ _dump_\) to that can be used to create your own replica, using the `restore` ElasticSearch API.

**It is important to note** that this snapshot is different from the files availables on our [Downloads page](http://www.targetvalidation.org/downloads/data). Those evidence and association files are the product of a pre-processed export through our Rest API \([http://api.opentargets.io/v3/platform/docs](https://urldefense.proofpoint.com/v2/url?u=http-3A__api.opentargets.io_v3_platform_docs&d=DwMFAw&c=n7UHtw8cUfEZZQ61ciL2BA&r=ZhzBE4adkrwWFCLwUz8sl2L08pOinkSBPT2-kXiY-Ls&m=kH1T4SDn11hFQ5Rsq4SaY01V95F6paxQ3cd3ENufcWQ&s=WJWMFx9Gjum2gFZIOciZVlBA6cA5CTRIBZxPbxpsGDY&e=)\) using our python client \([https://github.com/opentargets/opentargets-py](https://urldefense.proofpoint.com/v2/url?u=https-3A__github.com_opentargets_opentargets-2Dpy&d=DwMFAw&c=n7UHtw8cUfEZZQ61ciL2BA&r=ZhzBE4adkrwWFCLwUz8sl2L08pOinkSBPT2-kXiY-Ls&m=kH1T4SDn11hFQ5Rsq4SaY01V95F6paxQ3cd3ENufcWQ&s=tG-jseMMiXHvfQf3DOh2b4TQO2KOCBYVdh4T6ktJKvE&e=)\). They cannot be used to restore our application. Although these files are not a database dump per se, they have been formatted and can serve as inputs for your in-house tools: each line represents a fully dumped \(serialised to a string\) JSON-object independent of each other

## How to restore using the public snapshot

### Pre-requisites:

* docker \(on mac osx you can install the [docker for mac](https://docs.docker.com/docker-for-mac/) app \)

### Elasticsearch

Assuming you are following the official instructions and use [docker to run elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/docker.html), you can trigger the snapshot restore following these steps:

1\) create a docker volume as recommended:

```
docker volume create otdata
```

Check that it's been created:

```
docker volume inspect otdata
```

Also create a docker network that our docker containers will communicate through.

```
docker network create otnet
```

2\) Whitelist the url of our repo when you \`docker run\` by passing an environment variable:

```
docker run -d --name elastic --network otnet -p 9200:9200 -v otdata:/usr/share/elasticsearch/daata -e 'discovery.type=single-node' -e 'xpack.security.enabled=false' -e 'repositories.url.allowed_urls=https://storage.googleapis.com/*' docker.elastic.co/elasticsearch/elasticsearch:5.6.8
```

If you get a "invalid reference format" error, doublecheck that the container tag has not changed by visiting the elasticsearch [docker container listings](https://www.docker.elastic.co/). It can also happen as a result of  copy/pasting the command from this documentation page. Try to re-type in your own shell.

You can check that the docker container is running by typing `docker ps` and make sure ES is responding on the 9200 port by typing `curl localhost:9200` which should return a 200 response similar to:

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

3\) We now have to register the Open Targets public snapshot as a repo.

The URL for the latest ES snapshot \(i.e. Dec 2017\) is:

`https://storage.googleapis.com/open-targets-data-releases/17.12/17.12_snapshot/`

\(please be aware of the size of the snapshot, which is roughly 100GB\).

Again [following the elasticsearch documentation](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/modules-snapshots.html#_repositories) - you register the repo using this URL :

```
curl -XPUT 'localhost:9200/_snapshot/ot_repo?verify=false&pretty' -H 'Content-Type: application/json' -d'{
"type": "url",
"settings": {
"url": "https://storage.googleapis.com/open-targets-data-releases/17.12/17.12_snapshot/"
}}'
```

which should return:

```
{
  "acknowledged" : true
}
```

4\) find out the snapshots contained in the repo we just registered:

```
 curl localhost:9200/_cat/snapshots/ot_repo
```

which should return something similar to:

```
curator-20180126111418 SUCCESS 1516965258 11:14:18 1516967082 11:44:42 30.3m 12 24 0 24
```

Make a note of the name, which is the first field on the left, as we are going to use it in the next command.

5\) when the last step completes succesfully, you can [trigger the snapshot restore:](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/modules-snapshots.html#_restore)

`curl -XPOST 'localhost:9200/_snapshot/ot_repo/<snapshot name> /_restore?pretty'`

using the name from the step above

6\) Check the progress of the restore by looking at the \`\`\_cat/recovery\`\`\`

```
curl 'localhost:9200/_cat/recovery?v&h=index,time,type,stage,files_percent'
```

### REST API

To spin up a docker container running the Open Targets API, follow the [instruction on our README](https://github.com/opentargets/rest_api#run).

Basically:

```
docker run -d -p 8080:80 --network otnet --name rest_api -e "ELASTICSEARCH_URL=http://elastic:9200" -e "OPENTARGETS_DATA_VERSION=17.12" --privileged quay.io/opentargets/rest_api
```

**Check that is running: **

Supposing the container runs in`localhost`and expose port`8080`, you should get a 200 response from: [http://localhost:8080/v3/platform/public/utils/ping](http://localhost:8080/v3/platform/public/utils/ping)

From the command line, you can see if the API is alive with`curl localhost:8080/v3/platform/public/utils/ping`

and readiness can be checked by calling: `curl localhost:8080/v3/platform/public/utils/ping`

### Web application

To spin up a docker container running the Open Targets web app, follow the [instruction on the webapp README](https://github.com/opentargets/webapp#deploy-using-our-docker-container). Basically:

```
docker run -d --name webapp --network otnet -p 8443:443 -e "REST_API_SCHEME=https" -e "REST_API_SERVER=rest_api" -e "REST_API_PORT=443" quay.io/opentargets/webapp
```

## Add your own data

See the [related FAQ](/faq/add-your-own-data.md).

