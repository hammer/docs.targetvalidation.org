# How can I spin my own instance of the Platform?

The Open Targets Platform core stack is composed of three tiers:

1. a client-side [web application](https://github.com/opentargets/webapp)
2. a [REST API](https://github.com/opentargets/rest_api)
3. an ElasticSearch database

The web application communicates with the REST API, which in turn retrieves and queries the data from the ElasticSearch database.

For each release of the Open Targets Platform, you will have ElasticSearch snapshot \(i.e. a database dump\) so that it can be used to create your own instance if you use the `restore` ElasticSearch API.

N**ote:** our snapshot is different from the files available on the [Downloads](http://www.targetvalidation.org/downloads/data) page. The evidence and association files are the product of a pre-processed export through the Open Targets Platform [REST API](https://docs.targetvalidation.org/tutorials/rest-api) using the Open Targets Platform [Python client](https://docs.targetvalidation.org/programmatic-access/python-client). These files cannot be used to restore our application. Although these files are not a database dump _per se_, they have been formatted and can serve as inputs for your in-house tools. In these files, each line represents a fully dumped and serialised to a string JSON-object, which is independent of each other.

## How to restore using the public snapshot

#### Pre-requisites:

* Docker \(for Mac OS X, please install [docker for mac](https://docs.docker.com/docker-for-mac/)\)

### Elasticsearch

Assuming you are following the official instructions and use [docker to run elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/docker.html), you can trigger the snapshot restore following these steps:

1\) Create a docker volume as recommended:

```bash
docker volume create otdata
```

Check that it's been created:

```bash
docker volume inspect otdata
```

Also create a docker network that our docker containers will communicate through.

```bash
docker network create otnet
```

2\) Whitelist the URL of our repo when you \`docker run\` by passing an environment variable:

```bash
docker run -d --name elastic --network otnet -p 9200:9200 -v otdata:/usr/share/elasticsearch/data -e 'discovery.type=single-node' -e 'xpack.security.enabled=false' -e 'repositories.url.allowed_urls=https://storage.googleapis.com/*' docker.elastic.co/elasticsearch/elasticsearch:7.2.0
```

If you get a "invalid reference format" error, double check that the container tag has not changed. You can do so by visiting the elasticsearch [docker container listings](https://www.docker.elastic.co/). It can also happen as a result of copying/pasting the command from this documentation page. Try to re-type it in your own shell.

You can check that the docker container is running by typing `docker ps` . Make sure ES is responding on the 9200 port by typing `curl localhost:9200` . This which should return a 200 response similar to:

```text
{
  "name" : "72abdd2badd8",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "nPv5F8rdQZGN2DkeBQap3w",
  "version" : {
    "number" : "7.2.0",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "508c38a",
    "build_date" : "2019-06-20T15:54:18.811730Z",
    "build_snapshot" : false,
    "lucene_version" : "8.0.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```

More details on why you have to specify `repositories.url.allowed_urls` can be found in the official [elasticsearch documentation on read only URL repositories](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/modules-snapshots.html#_read_only_url_repository).

3\) You now have to register the Open Targets public snapshot as a repo.

The URL for the latest ES snapshot \(i.e. September 2019\) is https://storage.googleapis.com/open-targets-data-releases/19.09/output/es\_snapshot/ 

{% hint style="danger" %}
Please be aware of the size of the ES snapshot, which is roughly 100GB\)!
{% endhint %}

Register the repo using the URL below:

```bash
curl -XPUT 'localhost:9200/_snapshot/ot_repo?verify=false&pretty' -H 'Content-Type: application/json' -d'{
"type": "url",
"settings": {
"url": "https://storage.googleapis.com/open-targets-data-releases/19.09/output/es_snapshot/"
}}'
```

This should return:

```text
{
  "acknowledged" : true
}
```

4\) Find out the snapshots contained in the repo we have just registered:

```bash
 curl localhost:9200/_cat/snapshots/ot_repo
```

This should return something similar to:

```text
19.09 SUCCESS 1568799762 09:42:42 1568802285 10:24:45 42m 12 225 0 225
```

Make a note of the name above, which is the first field on the left, as we will use it in the next command.

5\) Once the last step completes successfully, you will [trigger the snapshot restore:](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/modules-snapshots.html#_restore)

{% code-tabs %}
{% code-tabs-item title="start\_restore" %}
```bash
curl -XPOST 'localhost:9200/_snapshot/ot_repo/19.09/_restore?pretty' -H 'Content-Type: application/json' -d'
{
  "indices": "*",
  "ignore_unavailable": true,
  "include_global_state": false
}
'

```
{% endcode-tabs-item %}
{% endcode-tabs %}

by using the `snapshot name` from the step above

6\) Check the progress of the restore by looking at the `_cat/recovery`

```bash
curl 'localhost:9200/_cat/recovery?v&h=index,time,type,stage,files_percent'
```

{% hint style="info" %}
If your restore operation fails for any reason halfway through, you can launch another restore operation after closing all indices with 

`curl -X POST "localhost:9200/_all/_close"`

and then reusing the `start_restore` command above.
{% endhint %}

{% hint style="danger" %}
If you are spinning versions of the Open Targets Platform snapshots from any release up and including 19.06, you should use ElasticSearch 5.6.13
{% endhint %}

### REST API

To spin up a docker container running the Open Targets API, follow the instruction on our README.

```text
docker run -d -p 8080:80 --network otnet --name rest_api -e "ELASTICSEARCH_URL=http://elastic:9200" -e "OPENTARGETS_DATA_VERSION=19.09" --privileged quay.io/opentargets/rest_api:19.09.5
```

**Check if the container is running:** 

If the container runs in`localhost`and expose port`8080`, you should get a 200 response from:

[http://localhost:8080/v3/platform/public/utils/ping](http://localhost:8080/v3/platform/public/utils/ping)

From the command line, you can see if the API is alive with`curl localhost:8080/v3/platform/public/utils/ping`

and readiness can be checked by calling: `curl localhost:8080/v3/platform/public/utils/ping`

### Web application

To spin up a docker container running the Open Targets web app, follow the [instruction on the webapp README](https://github.com/opentargets/webapp#deploy-using-our-docker-container):

```text
docker run -d --name webapp --network otnet -p 8443:443 -e "REST_API_SCHEME=https" -e "REST_API_SERVER=rest_api" -e "REST_API_PORT=443" quay.io/opentargets/webapp:19.09.5
```

