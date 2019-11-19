# How to get more than 10K targets associated with one disease

The maximum amount of results that the [Open Targets Platform REST API ](https://platform-api.opentargets.io/v3/platform/docs/swagger-ui)can return in each call is 10,000, but for some diseases such as [breast carcinoma](https://www.targetvalidation.org/disease/EFO_0000305/associations) \(EFO\_0000305\), the number of associated targets is beyond this limit.

How can you retrieve all the associations for a disease that contains more than 10,000 targets? Use `next`, a root-level field that contains a vector of elements to act as a token. If you add `next` when calling our API endpoints, such as the [`association/filter`](https://platform-api.opentargets.io/v3/platform/docs/swagger-ui#/filter/getAssociationFilter),  you will implement pagination and retrieve the next chunk of results.

{% hint style="info" %}
Head to our blog, for more details on [pagination](http://blog.opentargets.org/2017/11/06/discovering-drug-targets-gets-faster-our-api-upgrades-to-v3/#pagination) of larger set of results returned by the Open Targets Platform REST API.
{% endhint %}

You can use `next` in either **GET** or **POST** methods:

* **GET** - you will need to append the elements from the previous array to the next one
* **POST** - you will need to add  `next` as a JSON by inserting it as it is in the JSON payload structure

{% hint style="info" %}
Please note, that although you can use `next`, we would still recommend not retrieving more than 10K results in each call. If you would like to access all targets in the Open Targets Platform \(over 20,000\), please go to our [Data Download](https://www.targetvalidation.org/downloads/data) page to download the entire dataset.
{% endhint %}

Firstly, let's look at one example with the **GET** method using the command line.

In a terminal window, you can use CURL and the following line to retrieve the first 100 associations in JSON format

```text
curl -X GET 'https://platform-api.opentargets.io/v3/platform/public/association/filter?size=100&disease=EFO_0000305'
```

{% hint style="info" %}
Note that we are only retrieving **100** results at a time, not **10,000,** for a quicker response in this tutorial. 
{% endhint %}

To get the elements for the next 100 associations, install [jq](https://stedolan.github.io/jq/) and use `| jq 'next'`  as below:

```text
curl -X GET 'https://platform-api.opentargets.io/v3/platform/public/association/filter?size=100&disease=EFO_0000305'| jq '.next'
```

This is the response you will get:

> 1.128754**,**
>
>  **** "ENSG00000108840-EFO\_0000305"

To retrieve the next set of 100 results, you will use the elements returned in the first array above \(i.e. `1.128754`and `ENSG00000108840-EFO_0000305`\)  in addition to `&next=` for each of these elements to make the following call:

```text
curl -X GET 'https://platform-api.opentargets.io/v3/platform/public/association/filter?size=100&disease=EFO_0000305&next=1.128754&next=ENSG00000103089-EFO_0000305' | jq '.next'
```

You will get these elements:

> 0.988788**,**
>
>  **** "ENSG00000212993-EFO\_0000305"

To fetch the next set of results, you will append the elements from the call above to the next one, and so on so forth.

We can now look at using the **POST** method to retrieve the targets for breast carcinoma \(EFO\_0000305\). You will need to add  `next` in the JSON payload structure as shown below:

```text
curl -X POST 'https://platform-api.opentargets.io/v3/platform/public/association/filter?disease=EFO_0000305' @payload.json
```

> \# payload.json content  
> \# {  
> \#     "next": \[0.98741496,"ENSG00000118046-EFO\_0000305"\],  
> \#     "size": 100  
> \# }
>
> \`\`\`

​If you want to discuss this in more detail or request additional REST API tutorials, [email us](mailto:support@targetvalidation.org) and we will be happy to help.

  
  
  


