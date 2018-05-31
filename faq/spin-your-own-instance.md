# How can I spin my own instance of the Platform?

Our core stack is composed of three tiers:

1. a client-side [web application](https://github.com/opentargets/webapp) that communicates with 
2. a [Rest API](https://github.com/opentargets/rest_api) \([https://github.com/opentargets/rest\_api\](https://github.com/opentargets/rest_api%29\) which retrieves and queries the data from 
3. an ElasticSearch database; 

For each release of our Platform, you will have ElasticSearch snapshot \(i.e. a _database_ _dump_\) so that it can be used to create your own instance if you use the `restore` ElasticSearch API.

N**ote:** our snapshot is different from the files available on our [Downloads](http://www.targetvalidation.org/downloads/data) page. Those evidence and association files are the product of a pre-processed export through our [REST API](http://api.opentargets.io/v3/platform/docs) using our [Python](https://github.com/opentargets/opentargets-py) client. These files cannot be used to restore our application. Although these files are not a database dump _per se_, they have been formatted and can serve as inputs for your in-house tools. In these files, each line represents a fully dumped and serialised to a string JSON-object, which is independent of each other.

## How to restore using the public snapshot

#### Pre-requisites:

* Docker \(for Mac OS X, please install [docker for mac](https://docs.docker.com/docker-for-mac/)\)

### Elasticsearch

Assuming you are following the official instructions and use [docker to run elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/docker.html), you can trigger the snapshot restore following these steps:

1\) Create a docker volume as recommended:

```text
docker volume create otdata
```

Check that it's been created:

```text
docker volume inspect otdata
```

Also create a docker network that our docker containers will communicate through.

```text
docker network create otnet
```

2\) Whitelist the URL of our repo when you \`docker run\` by passing an environment variable:

```text
docker run -d --name elastic --network otnet -p 9200:9200 -v otdata:/usr/share/elasticsearch/daata -e 'discovery.type=single-node' -e 'xpack.security.enabled=false' -e 'repositories.url.allowed_urls=https://storage.googleapis.com/*' docker.elastic.co/elasticsearch/elasticsearch:5.6.8
```

If you get a "invalid reference format" error, double check that the container tag has not changed. You can do so by visiting the elasticsearch [docker container listings](https://www.docker.elastic.co/). It can also happen as a result of copying/pasting the command from this documentation page. Try to re-type it in your own shell.

You can check that the docker container is running by typing `docker ps` . Make sure ES is responding on the 9200 port by typing `curl localhost:9200` . This which should return a 200 response similar to:

```text
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

More details on why you have to specify `repositories.url.allowed_urls` can be found in the official [elasticsearch documentation on read only URL repositories](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/modules-snapshots.html#_read_only_url_repository).

3\) You now have to register the Open Targets public snapshot as a repo.

The URL for the latest ES snapshot \(i.e. Apr 2018\) is:

`https://storage.googleapis.com/open-targets-data-releases/18.04/18.04_snapshot/`

\(please be aware of the size of the snapshot, which is roughly 100GB\).

Register the repo using the URL below:

```text
curl -XPUT 'localhost:9200/_snapshot/ot_repo?verify=false&pretty' -H 'Content-Type: application/json' -d'{
"type": "url",
"settings": {
"url": "https://storage.googleapis.com/open-targets-data-releases/18.04/18.04_snapshot/"
}}'
```

This should return:

```text
{
  "acknowledged" : true
}
```

4\) Find out the snapshots contained in the repo we have just registered:

```text
 curl localhost:9200/_cat/snapshots/ot_repo
```

This should return something similar to:

```text
curator-20180126111418 SUCCESS 1516965258 11:14:18 1516967082 11:44:42 30.3m 12 24 0 24
```

Make a note of the name above, which is the first field on the left, as we will use it in the next command.

5\) Once the last step completes successfully, you will [trigger the snapshot restore:](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/modules-snapshots.html#_restore)

```text
curl -XPOST 'localhost:9200/_snapshot/ot_repo/curator-20180508094844/_restore?pretty' -H 'Content-Type: application/json' -d'
{
  "indices": "*",
  "ignore_unavailable": true,
  "include_global_state": false
}
'
```

by using the `snapshot name` from the step above

6\) Check the progress of the restore by looking at the `_cat/recovery`

```text
curl 'localhost:9200/_cat/recovery?v&h=index,time,type,stage,files_percent'
```

### REST API

To spin up a docker container running the Open Targets API, follow the instruction on our README.

```text
docker run -d -p 8080:80 --network otnet --name rest_api -e "ELASTICSEARCH_URL=http://elastic:9200" -e "OPENTARGETS_DATA_VERSION=18.04" --privileged quay.io/opentargets/rest_api
```

**Check if the container is running:** 

If the container runs in`localhost`and expose port`8080`, you should get a 200 response from:

[http://localhost:8080/v3/platform/public/utils/ping](http://localhost:8080/v3/platform/public/utils/ping)

From the command line, you can see if the API is alive with`curl localhost:8080/v3/platform/public/utils/ping`

and readiness can be checked by calling: `curl localhost:8080/v3/platform/public/utils/ping`

### Web application

To spin up a docker container running the Open Targets web app, follow the [instruction on the webapp README](https://github.com/opentargets/webapp#deploy-using-our-docker-container):

```text
docker run -d --name webapp --network otnet -p 8443:443 -e "REST_API_SCHEME=https" -e "REST_API_SERVER=rest_api" -e "REST_API_PORT=443" quay.io/opentargets/webapp
```

## Add your own data

See our [FAQ](https://legacy.gitbook.com/book/opentargets/docs/edit#/edit/master/faq/add-your-own-data.md?_k=3rnm61).

