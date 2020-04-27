# Target safety

Target safety assessments help understand the role of a drug target in normal physiology, and any potential unintended adverse consequences \(safety liabilities\) of target modulation \([Brennan 2017](https://link.springer.com/protocol/10.1007%2F978-1-4939-7172-5_12)\).

We perform manual curation of experimental data available from the literature and other resources of toxicity. Target safety data is subdivided into three categories:

* Known side effects
* Safety risk information 
* Non-clinical experimental toxicity

### Known side effects

Known side effects were manually curated from [Bowes et al. \(2012\)](https://europepmc.org/article/MED/23197038), [Urban et al. \(2012\)](https://onlinelibrary.wiley.com/doi/abs/10.1002/9781118098141.ch2), [Lamore et al. \(2017\)](https://europepmc.org/article/MED/28453775), [Lynch et al. \(2017\)](https://europepmc.org/article/MED/28216264), and [HeCaToS](https://www.hecatos.eu/).

Gene names were converted into Ensembl Gene IDs, main organs \(or systems affected\) were mapped to the [Uber-anatomy ontology](https://www.ebi.ac.uk/ols/ontologies/uberon), and source terms \(e.g. atrial fibrillation, cardiomyopathy\) were mapped to the Experimental Factor Ontology.

### **Safety risk information**

Safety risk information was manually curated from two sources, namely [Force and Kolaja \(2011\)](https://europepmc.org/article/MED/21283106) and HeCaToS.

Gene names were converted into Ensembl Gene IDs and main organs \(or systems affected\) were mapped to the [Uber-anatomy ontology](https://www.ebi.ac.uk/ols/ontologies/uberon).

### **Non-clinical experimental toxicity** 

#### **Tox21**

Data from the Tox21 data set is available [here](https://tripod.nih.gov/tox21/assays/index.html). Raw data was downloaded from the United States Environmental Protection Agency FTP site on 3rd December 2019. This data set comprises experimental toxicology data from publications selected by the Tox21 initiative as well as industry legacy reports. The data curation steps involved selecting target-centric experimental data points and excluding any data that did not report any toxicity parameters. Gene names were mapped to Ensembl identifiers and identity disambiguation was carried out using the UniProt identity mapping tool, the Ensembl website with cross reference with HGNC.

#### eTOX

The eTOX project is an Innovative Medicines Initiative dedicated to extracting and sharing preclinical study data. More information on this initiative can be found [here](https://www.mdpi.com/1422-0067/15/11/21136/htm)**.** The data sourced within the project was from scientific publications and legacy toxicology data from 13 participant pharmaceutical companies. Experimental information for human data targets was retrieved from the [EPA website](https://www.epa.gov/chemical-research/exploring-toxcast-data-downloadable-data) \(E-TOX\_Protein\_compilation data\) set on 25th November 2019. The data set was standardised for identifiers mapping all target information to Ensembl identifiers. Experimental information with toxicity related tissue and organ system was standardised according to the [CDISC SEND Controlled Terminology](https://evs.nci.nih.gov/ftp1/CDISC/SEND/SEND%20Terminology.html).

### **How to access this data**

Data on target safety is available for 439 targets and you can access this data via the:

* Open Targets Platform website e.g. in the profile pages for [PAX6](https://www.targetvalidation.org/target/ENSG00000007372) and [TBXA2R](https://www.targetvalidation.org/target/ENSG00000006638) 
* Open Targets Platform [REST API](https://docs.targetvalidation.org/programmatic-access/rest-api), using the [`private/target`](https://platform-api.opentargets.io/v3/platform/docs/swagger-ui#/private/getTargetByENSGID) endpoint
* [Data Download](https://www.targetvalidation.org/downloads/data) page

{% hint style="info" %}
Looking for significant adverse drug reactions \(ADRs\) instead? Check our [pharmacovigilance](https://docs.targetvalidation.org/getting-started/getting-started/drug-summary/pharmacovigilance) page.
{% endhint %}

