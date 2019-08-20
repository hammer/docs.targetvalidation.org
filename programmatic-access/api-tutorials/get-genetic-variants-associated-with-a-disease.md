# Get genetic variants associated with a disease with the Python client

This is an example on how you can get the genetic variants \(evidence\) associated with a disease of interest using the [Open Targets Python client](https://opentargets.readthedocs.io/en/stable/). This example highlights the filtering capabilities included in the client.

Check the [Open Targets Platform REST API](https://api.opentargets.io/v3/platform/docs/swagger-ui) documentation for more details.

Firstly, create a virtual environment:

```text
virtualenv venv
source venv/bin/activate
```

Then, install our Python client:

`pip install opentargets`

Now, choose your favourite editor and create a `get_genetic_evidence_for_disease.py` file that contains the code below:

```text
from opentargets import OpenTargetsClient
import argparse
import pandas as pd

parser = argparse.ArgumentParser(description='Retrieve SNPs and other genetic associations which are linked to a given disease')
parser.add_argument('disease',
                help='the disease of interest')
args = parser.parse_args()

ot = OpenTargetsClient()

e_for_disease = ot.get_evidence_for_disease(args.disease)
e_for_disease.filter(datatype='genetic_association')
print(e_for_disease)

outfilepath = 'genetic_evidence_associated_with_' + args.disease + '.csv'
pd.DataFrame([x['unique_association_fields'] for x in e_for_disease]).to_csv(outfilepath)
```

You can now run it by typing the following on the command line \(notice the quotes around the disease name\):

`(venv)$ python get_genetic_evidence_for_disease.py "neuropathic pain"`

Your folder will now contain a CSV file with the genetic evidence connected to neuropathic pain:

```text
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



