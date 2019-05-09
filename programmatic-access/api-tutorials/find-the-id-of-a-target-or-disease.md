# Find the ID of a target or disease

To use the Open Targets Platform REST API, you need to enter the Ensembl gene ID for a given target and the disease ID \(EFO, Orphanet, Human Phenotype Ontology\) for a disease of interest.

Use the [/search](https://api.opentargets.io/v3/platform/docs/swagger-ui#/search) endpoint to look for the identifier \(ID\) of the target or diseases of interest using a free text search such as NOD2 \(target\) or Crohn's disease \(disease\). 

{% hint style="info" %}
The `/search` endpoint should be used to identify the best match for a disease or target of interest. It will not give you details on the associations or evidence available for the target or disease of interest.
{% endhint %}

You can obtain the same result in Python by parsing the JSON as a dictionary and finding the correct index:

> ```text
> >>> import requests
> >>> from pprint import pprint
> >>> r = requests.get('https://platform-api.opentargets.io/v3/platform/public/search',
> params={"q":"NOD2","size":1})
> >>> pprint(r.json())
>
> {'data': [{'data': {'approved_name': 'nucleotide binding oligomerization '
>                                      'domain containing 2',
>                     'approved_symbol': 'NOD2',
>                     'association_counts': {'direct': 221, 'total': 380},
>                     'biotype': 'protein_coding',
>                     'description': 'Involved in ...',
>                     'ensembl_gene_id': 'ENSG00000167207',
> ```

which should return the expected JSON object. To select specific keys, you needs to traverse the resulting dictionary.

```text
>>> r.json()['data'][0]['id']
'ENSG00000167207'
```

{% hint style="info" %}
The `/search` endpoint replicates the functionality of the search box on the Open Targets Platform and will give the same results you get with our user interface.
{% endhint %}

