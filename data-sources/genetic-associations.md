# Genetic associations

Genetic associations are available for both common and rare \(Mendelian\) diseases and come from six data sources summarised below.

## Common diseases

### Open Targets Genetics portal

Genome wide association studies (GWAS) provide a link between common diseases and genomic loci, where each association is represented by a lead variant where the evidence for the association is the strongest, based on the reported p-value. The lead variant is not necessarily the causal (or the only causal) variant for the association. Moreover, the causal gene(s) is not necessarily the closest to the lead variant. Due to these reasons, identifying target-disease associations based on GWAS data is extremely challenging. Open Targets Genetics has been developed to address these challenges. Firstly, the Open Targets Genetics pipeline identifies tag variants from the lead (reported) variant through LD expansion or fine mapping, the latter for when summary statistics are available (e.g. UK Biobank and some GWAS curated by NHGRI-EBI GWAS Catalog). Once the set of tag variants are identified, Open Targets Genetics then uses a machine learning method to link the associated locus to the most likely causal gene(s) by integrating and summarising the effect of tag variants based on  genetic and functional genomic data namely:
* Expression QTLs
* Protein abundance QTLs
* Chromatin interaction 
* In silico prediction of variant functional consequence
* Distance of the variant to the transcript start site of the gene 


The weight of an evidence is given by the locus to gene score describing the likelihood of the gene being causal for the associated locus.

For more details, check Open Targets Genetics [overview](https://genetics-docs.opentargets.org/our-approach/pipeline-overview). 

The Genetics portal import summary statistics and manually curated lead variants from the NHGRI-EBI [GWAS Catalog](https://www.ebi.ac.uk/gwas) and UK Biobank summary statistics from the [Neale lab](http://www.nealelab.is/uk-biobank). In order to generate evidence connecting targets with diseases, significant GWAS associations (p-value < 5\*10^-8) are assigned to the most likely causal gene(s) using the L2G machine learning method. The score provided by the method is used for [evidence scoring](https://docs.targetvalidation.org/getting-started/scoring).

From February 2020 genome-wide association based evidence is sourced from the [Open Targets Genetics portal](https://genetics.opentargets.org/).


### PheWAS catalog

The [PheWAS](https://phewascatalog.org/) \(phenome-wide association studies\) resources provide associations between a genetic variant and multiple phenotypes. It contains clinical phenotypes derived from the electronic medical record \(EMR\)-linked DNA biobank BioVU by the Center for Precision Medicine at the Vanderbilt University Medical Centre. The EMR-based PheWAS uses ICD9 \(International Classification of Disease, 9th edition\), which were mapped to EFO using OLS and Zooma. The catalog contains all associations with p &lt; 0.05 \(uncorrected\).

## Rare \(Mendelian\) diseases

### UniProt

The Universal Protein Resource \([UniProt](http://www.uniprot.org/)\) provides protein sequence and functional information. It manually curates associations between genes and rare \(Mendelian\) diseases from literature and public databases. These curated variants must be in the coding region of a gene, deleterious, observed in patients, and segregating within their families.

### Genomics England PanelApp

The [Genomics England PanelApp](https://panelapp.extge.co.uk/crowdsourcing/PanelApp/) is a knowledgebase that combines crowdsourcing of expertise with curation to provide gene-disease relationships to aid the clinical interpretation of genomes within the 100,000 Genomes Project. This information is curated initially from four sources: Radboud University Medical Center, Illumina TruGenome Predisposition Screen, Emory Genetic Laboratory, and the UK Genetic Testing Network. The genes curated from at least three of these sources are initially classified as ‘green genes’. Additional sources may be used for the curation of some of the phenotypes, genes or mode of inheritance \(e.g. peer-reviewed published articles, OMIM, expert list\). Expert review of the gene panels for a particular disease is then sought in PanelApp, and each panel is revised. Only green diagnostic-grade genes on version 1+ panels \(which have the highest level of confidence\) are utilised for genome analysis within the 100,000 Genomes Project. We include in our Open Targets Platform the ‘green genes’ from version 1+ panels along with their phenotypes, providing the latter can be mapped to a disease or phenotype ontology.

### UniProt literature

UniProt may curate target-disease associations but not provide a specific mutation in the coding region of a gene. We classify these variants as UniProt Literature.

### European Variation Archive \(EVA\)

The EMBL-EBI [European Variation Archive](http://www.ebi.ac.uk/eva/?Home) \(EVA\) is a database of publicly available genetic variants, both short scale \(e.g. SNPs\) and large structural variants \(e.g. larger deletions\). For rare \(Mendelian\) diseases, EVA provides clinically relevant data for the variants that are pathogenic or likely pathogenic. This clinical information comes from [ClinVar](http://www.ncbi.nlm.nih.gov/clinvar/), and includes OMIM data.

### Gene2Phenotype

The data in [Gene2Phenotype](http://www.ebi.ac.uk/gene2phenotype) \(G2P\) is produced and curated from the literature by consultant clinical geneticists in the UK. This data is comprised of both short scale \(i.e. sequence variants such as SNPs\) and large structural variants \(e.g. copy number variants\), and can allow targeted filtering of genome-wide data for diagnostic purposes. The variants were provided by [DECIPHER](https://decipher.sanger.ac.uk/index), a database of genomic variants and phenotypes in patients with developmental disorders.

