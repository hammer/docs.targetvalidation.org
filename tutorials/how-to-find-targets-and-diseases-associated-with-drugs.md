---
description: >-
  We allow programmatic retrieval of our data via a set of REST services using
  the Open Targets Platform REST API.
---

# Diseases, targets and drugs

This is an example on how you can get the diseases associated with your targets of interest and their drug information using Python.

Check the [Open Targets Platform REST API](https://api.opentargets.io/v3/platform/docs/swagger-ui) documentation for more details.

```python
import pandas as pd
import request
```

```python
def drug_table(genelist):
    if len(genelist) > 100:
        print("You should split your list in chunks to not overload the API")
    drugfields = ['target.gene_info.symbol',
                  'target.target_class',
                  'evidence.target2drug.action_type',
                  'disease.efo_info.label',
                  'unique_association_fields.chembl_molecules',
                  'drug']
    payload = {"target":genelist, 'datatype':['known_drug'],'fields':drugfields}
    r = requests.post('https://api.opentargets.io/v3/platform/public/evidence/filter',
                      json=payload)

    for e in r.json()['data']:
        yield (e['target']['gene_info']['symbol'],
              e['target']['target_class'][0],
              e["unique_association_fields"]['chembl_molecules'],
              e['evidence']['target2drug']['action_type'],
              e['drug']['molecule_name'],
              e['drug']['molecule_type'],
              e['drug']["max_phase_for_all_diseases"]['numeric_index'],
              e['disease']['efo_info']['label'],
              )
```

Test that you can build a dataframe for one target

```python
cols = ['target','target_class','chembl_uri','moa','mol_name','mol_type','phase','indication']
brafdrugs = pd.DataFrame(drug_table(['ENSG00000157764']), columns=cols)
# drop duplicate evidence for each target-drug-indication combination
print(brafdrugs.shape)
brafdrugs.drop_duplicates(subset=['target','chembl_uri','indication'],inplace=True)
print(brafdrugs.shape)
brafdrugs
```

```text
(10, 8)
(6, 8)
```

  
    .dataframe tbody tr th:only-of-type {  
        vertical-align: middle;  
    }  
  
    .dataframe tbody tr th {  
        vertical-align: top;  
    }  
  
    .dataframe thead th {  
        text-align: right;  
    }  


|  | target | target\_class | chembl\_uri | moa | mol\_name | mol\_type | phase | indication |
| --- | --- | --- | --- | --- | --- | --- |
| 0 | BRAF | TKL protein kinase RAF family | http://identifiers.org/chembl.compound/CHEMBL2... | INHIBITOR | DABRAFENIB | Small molecule | 4 | neoplasm |
| 1 | BRAF | TKL protein kinase RAF family | http://identifiers.org/chembl.compound/CHEMBL1... | INHIBITOR | VEMURAFENIB | Small molecule | 4 | melanoma |
| 2 | BRAF | TKL protein kinase RAF family | http://identifiers.org/chembl.compound/CHEMBL1336 | INHIBITOR | SORAFENIB | Small molecule | 4 | hepatocellular carcinoma |
| 5 | BRAF | TKL protein kinase RAF family | http://identifiers.org/chembl.compound/CHEMBL1336 | INHIBITOR | SORAFENIB | Small molecule | 4 | neoplasm |
| 7 | BRAF | TKL protein kinase RAF family | http://identifiers.org/chembl.compound/CHEMBL1... | INHIBITOR | VEMURAFENIB | Small molecule | 4 | neoplasm |
| 8 | BRAF | TKL protein kinase RAF family | http://identifiers.org/chembl.compound/CHEMBL2... | INHIBITOR | DABRAFENIB | Small molecule | 4 | melanoma |



Now, if you want to do this for a list of genes as a text file:

```python
with open('input_genes.txt') as f:
    bcgenes = f.read().splitlines()
bcgenes[:5]
```

```text
['AARSD1', 'ABCA3', 'ABCB6', 'ABHD1', 'ABHD8']
```

Firstly,  you need to map your gene symbols to Ensembl gene IDs.

Here we use [MyGene.info](https://mygene.info/) as a quick lookup and annotation service. 

Head to their [ID mapping using mygene module in Python](http://nbviewer.jupyter.org/gist/newgene/6771106/id_mapping_mygene.ipynb) page to learn more about MyGene.

```python
import mygene

mg = mygene.MyGeneInfo()
mgres = mg.querymany(bcgenes, scopes='symbol,alias',fields='ensembl.gene', species='human')
```

```text
querying 1-1000...done.
querying 1001-1449...done.
Finished.
113 input query terms found dup hits:
    [('ACAT1', 2), ('ADCY3', 2), ('APITD1', 2), ('APOL3', 2), ('APP', 3), ('ARL17A', 3), ('ATP1A1', 3), 
14 input query terms found no hit:
    ['AL021546.6', 'CTC-236F12.4', 'CTC-260F20.3', 'CTD-2132N18.3', 'RP11-1167A19.2', 'RP11-145E5.5', 'R
Pass "returnall=True" to return complete lists of duplicate or missing query terms.
```

```python
bcgenes_ensg = []
for x in mgres:
    try:
        bcgenes_ensg.append(x['ensembl']['gene'])
    except KeyError:
        pass
    except TypeError:
        bcgenes_ensg.append(x['ensembl'][0]['gene'])
bcgenes_ensg[:3]
```

```text
['ENSG00000266967', 'ENSG00000167972', 'ENSG00000115657']
```

It is better to chunk this list not to overload the API:

```python
genes_chunked = [bcgenes_ensg[i:i + 50] for i in range(0, len(bcgenes_ensg), 50)]
```

Now we can make the dataframe of gene, drug, indication triples:

```python
drugtable = pd.concat([pd.DataFrame(drug_table(g), columns=cols) for g in genes_chunked])
```

```python
drugtable.head()
```

  
    .dataframe tbody tr th:only-of-type {  
        vertical-align: middle;  
    }  
  
    .dataframe tbody tr th {  
        vertical-align: top;  
    }  
  
    .dataframe thead th {  
        text-align: right;  
    }  


|  | target | target\_class | chembl\_uri | moa | mol\_name | mol\_type | phase | indication |
| --- | --- | --- | --- | --- | --- |
| 0 | ADORA1 | Adenosine receptor | http://identifiers.org/chembl.compound/CHEMBL190 | ANTAGONIST | THEOPHYLLINE | Small molecule | 4 | chronic obstructive pulmonary disease |
| 1 | ADORA1 | Adenosine receptor | http://identifiers.org/chembl.compound/CHEMBL113 | ANTAGONIST | CAFFEINE | Small molecule | 4 | ulcerative colitis |
| 2 | ADORA1 | Adenosine receptor | http://identifiers.org/chembl.compound/CHEMBL190 | ANTAGONIST | THEOPHYLLINE | Small molecule | 4 | asthma |
| 3 | ADORA1 | Adenosine receptor | http://identifiers.org/chembl.compound/CHEMBL190 | ANTAGONIST | THEOPHYLLINE | Small molecule | 4 | chronic obstructive pulmonary disease |
| 4 | ADORA1 | Adenosine receptor | http://identifiers.org/chembl.compound/CHEMBL190 | ANTAGONIST | THEOPHYLLINE | Small molecule | 4 | asthma |

```python
drugtable.to_excel('drug_table.xls')
```

{% hint style="info" %}
Check our "How to take a REST from manual searches with the Open Targets API" webinar below.
{% endhint %}

{% embed data="{\"url\":\"https://www.youtube.com/watch?v=KQbfhwpeEvc&list=PLncWVtwSXtqb8PyL6-ENSCuqP7\_4Aj5BE&index=2\",\"type\":\"video\",\"title\":\"EMBL-EBI programmatically: Open Targets\",\"description\":\"Open Targets is a partnership between academia and industry for systematic identification and prioritisation of new drug targets.\\nWe’ve developed a unique resource for free access to integrated biological data to enable drug target discovery, the Open Targets Platform. Our Platform provides gene and disease associations and detailed information on both genes and human diseases.\\n\\nIn this webinar, Denise Carvalho-Silva:\\n\\nIntroduces the Open Targets Platform \(0:46\)\\nGives an overview of modes of data access \(10:15\)\\nShows you where you can find the Open Targets API documentation \(13:57\)\\nProvide examples of REST API calls \(16:16\)\\nShows you how to query the REST server \(22:15\)\\n\\nDocumentation for the API can be found on the Open Targets website along with information about the Python client for the API.\\n\\nhttp://api.opentargets.io/v3/platform/docs\\n\\nYou can download the slides from the webinar in Train online.\\n\\nhttps://www.ebi.ac.uk/training/online/course/embl-ebi-programmatically-take-rest-manual-searches/open-targets-programmatically\\n\\nWant to know more about accessing EMBL-EBI resources programmatically? Have a look at the other webinars in this series:\\n\\nhttps://www.ebi.ac.uk/training/online/course/embl-ebi-programmatically-take-rest-manual-searches\",\"icon\":{\"type\":\"icon\",\"url\":\"https://www.youtube.com/yts/img/favicon\_144-vfliLAfaB.png\",\"width\":144,\"height\":144,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://i.ytimg.com/vi/KQbfhwpeEvc/mqdefault.jpg\",\"width\":320,\"height\":180,\"aspectRatio\":0.5625},\"embed\":{\"type\":\"player\",\"url\":\"https://www.youtube.com/embed/KQbfhwpeEvc?rel=0&showinfo=0\",\"html\":\"<div style=\\\"left: 0; width: 100%; height: 0; position: relative; padding-bottom: 56.2493%;\\\"><iframe src=\\\"https://www.youtube.com/embed/KQbfhwpeEvc?rel=0&amp;showinfo=0\\\" style=\\\"border: 0; top: 0; left: 0; width: 100%; height: 100%; position: absolute;\\\" allowfullscreen scrolling=\\\"no\\\"></iframe></div>\",\"aspectRatio\":1.7778}}" %}

