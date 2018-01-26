### Data Sources

* * [Somatic mutations](http://www.targetvalidation.org/#somatic_mutation)
  * [Cancer Gene Census](http://www.targetvalidation.org/#census)
  * [Uniprot somatic](http://www.targetvalidation.org/#uniprot_somatic)
  * [European Variation Archive \(EVA\)](http://www.targetvalidation.org/#eva_somatic)
  * [IntOGen](http://www.targetvalidation.org/#intogen)
* [Drugs](http://www.targetvalidation.org/#known_drug)
  * [Chembl](http://www.targetvalidation.org/#chembl)
* [Affected pathways](http://www.targetvalidation.org/#affected_pathway)
  * [Reactome](http://www.targetvalidation.org/#reactome)
  * [SLAPenrich](http://www.targetvalidation.org/#SLAPenrich)
* [RNA expression](http://www.targetvalidation.org/#rna_expression)
  * [Expression Atlas](http://www.targetvalidation.org/#atlas)
* [Text mining](http://www.targetvalidation.org/#literature)
  * [Europe PMC](http://www.targetvalidation.org/#text_mining)
* [Animal models](http://www.targetvalidation.org/#animal_model)
  * [PhenoDigm](http://www.targetvalidation.org/#mouse)

We collect data from various sources and combine them into categories called Data types to allow for target identification and prioritisation using our Open Targets Platform. We list our current data types and their data sources below. Note that data from an individual source can contribute to different Data types, e.g. data from EVA is observed in two data types, Genetic associations and Somatic mutations.

#### 

##### UniProt

The Universal Protein Resource \([UniProt](http://www.uniprot.org/)\) provides protein sequence and functional information. It manually curates associations between genes and rare \(Mendelian\) diseases from literature and public databases. These curated variants must be in the coding region of a gene, deleterious, observed in patients, and segregating within their families.

##### UniProt literature

UniProt may curate target-disease associations but not provide a specific mutation in the coding region of a gene. We classify these variants as UniProt Literature.

##### European Variation Archive \(EVA\)

The EMBL-EBI[European Variation Archive](http://www.ebi.ac.uk/eva/?Home)\(EVA\) is a database of publicly available genetic variants, both short scale \(e.g. SNPs\) and large structural variants \(e.g. larger deletions\). For rare \(Mendelian\) diseases, EVA provides clinically relevant data for the variants that are pathogenic or likely pathogenic. This clinical information comes from[ClinVar](http://www.ncbi.nlm.nih.gov/clinvar/), and includesOMIM data.

##### Gene2Phenotype

The data in[Gene2Phenotype](http://www.ebi.ac.uk/gene2phenotype)\(G2P\) is produced and curated from the literature by consultant clinical geneticists in the UK. This data is comprised of both short scale \(i.e. sequence variants such as SNPs\) and large structural variants \(e.g. copy number variants\), and can allow targeted filtering of genome-wide data for diagnostic purposes. The variants were provided by[DECIPHER](https://decipher.sanger.ac.uk/index), a database of genomic variants and phenotypes in patients with developmental disorders.

#### Somatic mutations

Somatic mutation data refers to mutations that may have clinical or treatment implications in cancer and possibly other diseases. This data type is obtained from the following sources:

##### Cancer Gene Census

Cancer Gene Census is a catalogue of genes for which mutations have been causally implicated in cancer. The Catalogue of Somatic Mutations in Cancer \([COSMIC](http://cancer.sanger.ac.uk/cosmic)\) at the Wellcome Trust Sanger Institute provides us with the set of genes associated with specific cancers in the Cancer Gene Census, in addition to other cancers associated with that gene in the COSMIC database.

##### Uniprot somatic

UniProt manually curates somatic mutations from the literature for our associations between genes and cancers.

##### European Variation Archive \(EVA\)

The EMBL-EBI[European Variation Archive](http://www.ebi.ac.uk/eva/?Home)\(EVA\) provides data on somatic mutations in both cancer and other diseases.

##### IntOGen

[IntOGen](http://www.intogen.org/search)provides somatic mutations, genes and pathways involved in tumorigenesis. We have imported the latest data from 6,792 samples across 28 cancer types \([Rubio-Perez et al](http://www.ncbi.nlm.nih.gov/pubmed/25759023)\). In these new dataset, false mutation calls have been filtered out and additional expression data is available for a larger number of samples in certain tumour types. This IntOgen analysis is updated and has not yet been released on the IntOgen website; so there can be discrepancies between targetvalidation.org and the IntOgen site.

#### Drugs

This data type is currently comprised of only one data source:

##### Chembl

The EMBL-EBI[ChEMBL](https://www.ebi.ac.uk/chembl/)database provides evidence from known drugs that can be linked to a disease and a known target. ChEMBL contains compound bioactivity data against drug targets. We display the data on drugs that have been approved for marketing by the U.S Food and Drug Administration \(FDA\), in addition to some clinical candidates.

#### Affected pathways

This data type contains pathway information on biochemical reactions sourced from the following sources:

##### Reactome

The[Reactome](http://www.reactome.org/)database manually curates and identifies reaction pathways that are affected by pathogenic mutations.

##### SLAPenrich

[SLAPenrich](https://saezlab.github.io/SLAPenrich/)\(Sample-population Level Analysis of Pathway enrichments\) is a novel statistical framework for the identification of significantly mutated pathways, at the sample population level, in large cohorts of cancer patients. It is based on a Poisson binomial model that takes into account the length of blocks of exons in genes within each pathway, and the background mutation rate of the analysed cohort of patients. We include in our Open Targets Platform the data obtained using SLAPenrich on somatic mutations from the The Cancer Genome Atlas across 25 different cancer types and a collection of pathway gene sets from Reactome.

#### RNA expression

This data type contains information on gene expression patterns under different biological conditions coming from the following resource:

##### Expression Atlas

The EMBL-EBI[Expression Atlas](https://www.ebi.ac.uk/gxa/home)provides information on genes that are differentially expressed. They report the changes on the levels of gene expression between normal and disease samples, or among disease samples from different studies. In addition to differential expression, they provide baseline expression information for each gene. This is available in the page containing the target profile.

#### Text mining

This data type contains evidence of target-disease association which is extracted automatically by mining the following literature database:

##### Europe PMC

The Europe PubMed Central \([Europe PMC](http://europepmc.org/)\) provides evidence of links between targets and diseases. They mine the titles, abstracts and full text research articles from both PubMed and PubMed Central, and use an entity-to-entity recognition approach to detect co-occurrences of target and disease entities.

#### Animal models

Model organisms are a valuable source for the characterisation and identification of disease-gene associations, especially when the molecular basis and/or function of the candidate target are unknown. We use the data on animal models from PhenoDigm:

##### PhenoDigm

The Wellcome Trust Sanger Institute[PhenoDigm](http://www.sanger.ac.uk/science/tools/phenodigm)database provides evidence on associations of targets and disease. It uses a semantic approach to map between clinical features observed in humans and mouse phenotype annotations. The phenotypic effects in mice are then mapped to phenotypes associated with human diseases, and matches are identified and scored.

