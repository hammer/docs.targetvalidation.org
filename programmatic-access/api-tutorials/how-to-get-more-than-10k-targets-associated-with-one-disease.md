# How to get more than 10K targets associated with one disease

The maximum amount of results that our [Open Targets Platform REST API ](https://platform-api.opentargets.io/v3/platform/docs/swagger-ui)returns in each call is 10,000, but for some diseases such as [brain disease](https://www.targetvalidation.org/disease/EFO_0005774/associations) \(EFO\_0005774\), the number of associated targets is beyond this limit.

How can you retrieve all the associations for a disease that contains more than 10,000 targets? Use `next`, a root-level field that contains a vector of elements to act as a token. If you add `next` when calling our API endpoints, such as the [`association/filter`](https://platform-api.opentargets.io/v3/platform/docs/swagger-ui#/filter/getAssociationFilter),  you will implement pagination and retrieve the next chunk of results.

You can use `next` in either **GET** or **POST** methods:

* GET - you will need to append the elements from the previous array to the next one
* POST - you will need to add  `next` as a JSON by inserting it as it is in the JSON payload structure

{% hint style="info" %}
Please note, that although you can use `next`, we would still recommend not retrieving more than 10K results in each call. If you would like to access the all targets in our Open Targets Platform \(over 20,000\), please go to our [Data Download](https://www.targetvalidation.org/downloads/data) page to download the entire dataset.
{% endhint %}

Let's look at one example with the **GET** method first:

```text
http GET 'https://platform-api.opentargets.io/v3/platform/public/association/filter?size=10000&disease=EFO_0005774'| jq '.next'
```

{% hint style="info" %}
Make sure you have `jq` installed for backtracking and managing JSON data.
{% endhint %}

You will get these elements:

> 0.015444**,**
>
>  **** "ENSG00000160193-EFO\_0005774"

To retrieve the following set of results, you will use the elements returned in the first array \(see above\) to make the next call:

```text
http GET 'https://platform-api.opentargets.io/v3/platform/public/association/filter?size=100&disease=EFO_0005774&next=0.015444&next=ENSG00000103089-EFO_0005774' | jq '.next'
```

You will get these elements:

> 0.0148**,**
>
>  **** "ENSG00000158715-EFO\_0005774"

To fetch the next set of results, you will append the elements from your previous call to the next one, and so on so forth.

Let's now try the **POST** method to retrieve the targets for cancer \(EFO\_0000311\):

```text
 http POST 'https://platform-api.opentargets.io/v3/platform/public/association/filter?disease=EFO_0000311
' @payload.json
```

> \# payload.json content  
> \# {  
> \#     "next": \[1.2693106,"ENSG00000151702-EFO\_0000311"\],  
> \#     "size": 100  
> \# }
>
> \`\`\`

​[Email us](mailto:support@targetvalidation.org) if you want to discuss this in more details or request additional tutorials using our REST API. Looking forward to hearing your suggestions.

  
  
  


