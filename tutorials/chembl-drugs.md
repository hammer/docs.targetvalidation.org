
## Get a list of drugs and indication for each target

We'll use the python client to get a list of compounds associated to targets and diseases:


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

    (10, 8)
    (6, 8)





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>target</th>
      <th>target_class</th>
      <th>chembl_uri</th>
      <th>moa</th>
      <th>mol_name</th>
      <th>mol_type</th>
      <th>phase</th>
      <th>indication</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BRAF</td>
      <td>TKL protein kinase RAF family</td>
      <td>http://identifiers.org/chembl.compound/CHEMBL2...</td>
      <td>INHIBITOR</td>
      <td>DABRAFENIB</td>
      <td>Small molecule</td>
      <td>4</td>
      <td>neoplasm</td>
    </tr>
    <tr>
      <th>1</th>
      <td>BRAF</td>
      <td>TKL protein kinase RAF family</td>
      <td>http://identifiers.org/chembl.compound/CHEMBL1...</td>
      <td>INHIBITOR</td>
      <td>VEMURAFENIB</td>
      <td>Small molecule</td>
      <td>4</td>
      <td>melanoma</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BRAF</td>
      <td>TKL protein kinase RAF family</td>
      <td>http://identifiers.org/chembl.compound/CHEMBL1336</td>
      <td>INHIBITOR</td>
      <td>SORAFENIB</td>
      <td>Small molecule</td>
      <td>4</td>
      <td>hepatocellular carcinoma</td>
    </tr>
    <tr>
      <th>5</th>
      <td>BRAF</td>
      <td>TKL protein kinase RAF family</td>
      <td>http://identifiers.org/chembl.compound/CHEMBL1336</td>
      <td>INHIBITOR</td>
      <td>SORAFENIB</td>
      <td>Small molecule</td>
      <td>4</td>
      <td>neoplasm</td>
    </tr>
    <tr>
      <th>7</th>
      <td>BRAF</td>
      <td>TKL protein kinase RAF family</td>
      <td>http://identifiers.org/chembl.compound/CHEMBL1...</td>
      <td>INHIBITOR</td>
      <td>VEMURAFENIB</td>
      <td>Small molecule</td>
      <td>4</td>
      <td>neoplasm</td>
    </tr>
    <tr>
      <th>8</th>
      <td>BRAF</td>
      <td>TKL protein kinase RAF family</td>
      <td>http://identifiers.org/chembl.compound/CHEMBL2...</td>
      <td>INHIBITOR</td>
      <td>DABRAFENIB</td>
      <td>Small molecule</td>
      <td>4</td>
      <td>melanoma</td>
    </tr>
  </tbody>
</table>
</div>



Now, we would like to do this for more than one gene at the time.

For example, you might have a list of genes in a text file:


```python
with open('input_genes.txt') as f:
    bcgenes = f.read().splitlines()
bcgenes[:5]
```




    ['AARSD1', 'ABCA3', 'ABCB6', 'ABHD1', 'ABHD8']



First, you will have to map your gene symbols to gene IDs. 

I am using here https://mygene.info which is a quick lookup and annotation service. 
You can read more at http://nbviewer.jupyter.org/gist/newgene/6771106



```python
import mygene

mg = mygene.MyGeneInfo()
mgres = mg.querymany(bcgenes, scopes='symbol,alias',fields='ensembl.gene', species='human')
```

    querying 1-1000...done.
    querying 1001-1449...done.
    Finished.
    113 input query terms found dup hits:
    	[('ACAT1', 2), ('ADCY3', 2), ('APITD1', 2), ('APOL3', 2), ('APP', 3), ('ARL17A', 3), ('ATP1A1', 3), 
    14 input query terms found no hit:
    	['AL021546.6', 'CTC-236F12.4', 'CTC-260F20.3', 'CTD-2132N18.3', 'RP11-1167A19.2', 'RP11-145E5.5', 'R
    Pass "returnall=True" to return complete lists of duplicate or missing query terms.



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




    ['ENSG00000266967', 'ENSG00000167972', 'ENSG00000115657']



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




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>target</th>
      <th>target_class</th>
      <th>chembl_uri</th>
      <th>moa</th>
      <th>mol_name</th>
      <th>mol_type</th>
      <th>phase</th>
      <th>indication</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ADORA1</td>
      <td>Adenosine receptor</td>
      <td>http://identifiers.org/chembl.compound/CHEMBL190</td>
      <td>ANTAGONIST</td>
      <td>THEOPHYLLINE</td>
      <td>Small molecule</td>
      <td>4</td>
      <td>chronic obstructive pulmonary disease</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ADORA1</td>
      <td>Adenosine receptor</td>
      <td>http://identifiers.org/chembl.compound/CHEMBL113</td>
      <td>ANTAGONIST</td>
      <td>CAFFEINE</td>
      <td>Small molecule</td>
      <td>4</td>
      <td>ulcerative colitis</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ADORA1</td>
      <td>Adenosine receptor</td>
      <td>http://identifiers.org/chembl.compound/CHEMBL190</td>
      <td>ANTAGONIST</td>
      <td>THEOPHYLLINE</td>
      <td>Small molecule</td>
      <td>4</td>
      <td>asthma</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ADORA1</td>
      <td>Adenosine receptor</td>
      <td>http://identifiers.org/chembl.compound/CHEMBL190</td>
      <td>ANTAGONIST</td>
      <td>THEOPHYLLINE</td>
      <td>Small molecule</td>
      <td>4</td>
      <td>chronic obstructive pulmonary disease</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ADORA1</td>
      <td>Adenosine receptor</td>
      <td>http://identifiers.org/chembl.compound/CHEMBL190</td>
      <td>ANTAGONIST</td>
      <td>THEOPHYLLINE</td>
      <td>Small molecule</td>
      <td>4</td>
      <td>asthma</td>
    </tr>
  </tbody>
</table>
</div>




```python
drugtable.to_excel('drug_table.xls')
```
