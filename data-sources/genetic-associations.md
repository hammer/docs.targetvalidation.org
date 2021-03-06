# Genetic associations

Genetic associations are available for both common and rare \(Mendelian\) diseases and come from six data sources summarised below.

## Common diseases

### GWAS catalog

The NHGRI-EBI [GWAS catalog](https://www.ebi.ac.uk/gwas/docs/about) provides evidence on the association of genes \(targets\) and common diseases. This data comes from the manual curation of published Genome Wide Association Studies \(GWAS\). The catalog gives a list of the genetic variants \(e.g. SNPs\) that are most associated with a disease, by genomic region. We include all associations with p-values ≤ 10-5, so that we broaden the coverage of diseases. We assess the link between variant and gene using the Open Targets custom annotation pipeline to find the association between a disease and its most likely target. Variants are assigned to a gene by first considering any deleterious consequence within the coding region of that gene, followed by whether the variant is located within introns or regulatory regions. If the variant is intergenic, it will be assigned to the promoter region of the nearest gene. The consequences of these [variants](http://targetvalidation.org/variants) are annotated using the [Variant Effect Predictor](http://www.ensembl.org/info/docs/tools/vep/index.html).

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

