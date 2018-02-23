## How can you download all the genetic association for a given phenotype or disease through the Open Targets API?

The easiest way is to use our [Open Targets Python client](https://github.com/opentargets/opentargets-py/). Let me guide you through a simple example that uses the filtering capabilities included in the client.

First, create a virtual environment:

```
virtualenv venv
source venv/bin/activate
```

Then, you should install our Python client:

`pip install opentargets`

Now, I will choose my favourite editor and create a `get_genetic_evidence_for_disease.py` file that contains the code below:

```
from opentargets import OpenTargetsClient
import argparse
import pandas as pd

parser = argparse.ArgumentParser(description='Retrieve SNPs and other genetic associations which are linked to a given disease')
parser.add_argument('disease',
                help='the disease of interest'\)
args = parser.parse_args()

ot = OpenTargetsClient()

e_for_disease = ot.get_evidence_for_disease(args.disease)
e_for_disease.filter(datatype='genetic_association')
print(e_for_disease)

outfilepath = 'genetic_evidence_associated_with_' + args.disease + '.csv'
pd.DataFrame([x['unique_association_fields'] for x in e_for_disease]).to_csv(outfilepath)
```

I can now run it by typing on the command line \(notice the quotes around the disease name\):

`(venv)$ python get_genetic_evidence_for_disease.py "neuropathic pain"`

My folder will now contain a CSV file with the genetic evidence connected to neuropathic pain:

```
,gwas_panel_resolution,object,pubmed_refs,pvalue,sample_size,study_name,target,variant
0,6906962,
http://www.ebi.ac.uk/efo/EFO_0005762,http://europepmc.org/abstract/MED/26629533,3e-7,4221,cttv009_gwas_catalog,http://identifiers.org/ensembl/ENSG00000121903,http://identifiers.org/dbsnp/rs71647933

1,6906962,
http://www.ebi.ac.uk/efo/EFO_0005762,http://europepmc.org/abstract/MED/26629533,4e-7,4221,cttv009_gwas_catalog,http://identifiers.org/ensembl/ENSG00000121903,http://identifiers.org/dbsnp/rs35260355

2,6906962,
http://www.ebi.ac.uk/efo/EFO_0005762,http://europepmc.org/abstract/MED/26629533,8e-7,4221,cttv009_gwas_catalog,http://identifiers.org/ensembl/ENSG00000174429,http://identifiers.org/dbsnp/rs6986153

3,6494962,
http://www.ebi.ac.uk/efo/EFO_0005762,http://europepmc.org/abstract/MED/24974787,2e-7,3063,cttv009_gwas_catalog,http://identifiers.org/ensembl/ENSG00000168546,http://identifiers.org/dbsnp/rs17428041

4,6494962,
http://www.ebi.ac.uk/efo/EFO_0005762,http://europepmc.org/abstract/MED/24974787,1e-6,3063,cttv009_gwas_catalog,http://identifiers.org/ensembl/ENSG00000185652,http://identifiers.org/dbsnp/rs11615866
```



