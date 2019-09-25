---
description: >-
  This data type contains pathway information on biochemical reactions sourced
  from four data sources summarised below.
---

# Pathways & systems biology

{% hint style="info" %}
This data type used to be displayed as `Affected pathways` in the user interface up to release 18.10 of the Open Targets Platform. It is now shown as "Pathways & systems biology".
{% endhint %}

### Reactome

The [Reactome](http://www.reactome.org/) database manually curates and identifies reaction pathways that are affected by pathogenic mutations.

### SLAPenrich

[SLAPenrich](https://saezlab.github.io/SLAPenrich/) \(Sample-population Level Analysis of Pathway enrichments\) is a novel statistical framework for the identification of significantly mutated pathways, at the sample population level, in large cohorts of cancer patients. It is based on a Poisson binomial model that takes into account the length of blocks of exons in genes within each pathway, and the background mutation rate of the analysed cohort of patients. We include in the Open Targets Platform the data obtained using SLAPenrich on somatic mutations from the The Cancer Genome Atlas \(TCGA\) across 25 different cancer types and a collection of pathway gene sets from Reactome. These 374 pathways are curated and mapped to cancer hallmarks.

See[ Iorio et al \(2018\)](https://europepmc.org/abstract/MED/29713020) for more details.

### PROGENy

[PROGENy](https://saezlab.github.io/progeny/) \(Pathway RespOnsive GENes\) is a linear regression model that calculates pathway activity based on consensus gene signatures obtained from perturbation experiments. We use PROGENy \([Schubert et al](https://www.nature.com/articles/s41467-017-02391-6.epdf?author_access_token=16QkzhJ3OA3qJDqBw_GvGdRgN0jAjWel9jnR3ZoTv0NBFLUVI-ebH2AmtFlR1ykSPIho7ETJXL7VqZFC4zGtU0BaeoZncGrwx3ZW24lfVqvbSWqsQKaUXFTi_c-4pgcpX-1qerWYlkG6sha8rhrnMg%3D%3D)\) for the systematic comparison of pathway activities between normal and primary samples from The Cancer Genome Atlas \(TCGA\). We include in the Open Targets Platform sample-level pathway activities inferred from RNA-seq for 9,250 tumour and 741 normal TCGA samples from 14 tumour types, and compute differential pathway activities between matched normal and tumour samples. We cover the following pathways: EGFR, hypoxia, JAK.STAT, MAPK, NFkB, PI3K, TGFb, TNFa, Trail, VEGF,  and p53. 

See [Schubert et al \(2018\)](https://europepmc.org/abstract/MED/29295995) for more details.

### Sysbio

Sysbio includes six gene lists curated from four systems biology analysis papers. These publications integrate different types of data to identify key drivers \(or regulators\) in the following diseases \(or phenotypes\):

* Inflammatory bowel disease \([PMID:28892060](https://europepmc.org/abstract/MED/28892060)\)
* Coronary heart disease \([PMID:23539213](https://europepmc.org/abstract/MED/23539213)\)
* Late-onset Alzheimer's disease \([PMID:23622250](https://europepmc.org/abstract/MED/23622250)\)
* Cognitive decline of Alzheimer's disease \([PMID:29802388](https://europepmc.org/abstract/MED/29802388)\)

### CRISPR

This datatype has been available since release 19.04, following the Nature publication [Prioritization of cancer therapeutic targets using CRISPR-Cas9 screens](https://europepmc.org/abstract/MED/30971826), where we have integrated gene fitness effects with tractability data and genomic biomarkers \(i.e. cancer driver events\) for a systematic prioritisation of targets in defined tissues and genotypes. 

In the Open Targets Platform, CRISPR data is used as evidence for the associations of 624 genes \(targets\) prioritised in 19 different cancer types, resulting in 1,846 target-disease associations. Genes with priority scores greater than 41.5 in [supplementary information](https://www.nature.com/articles/s41586-019-1103-9#Sec44) section in the Nature paper \("final score" column in the table 6\) are included in the Platform.







