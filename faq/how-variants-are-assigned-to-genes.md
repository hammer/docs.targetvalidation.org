# How variants are assigned to genes

We map and annotate variants to genes and transcripts using the Ensembl Variant Effect Predictor \(VEP\). If a variant maps to a gene with different transcripts, we will assign it the most severe [variant definitions](http://www.targetvalidation.org/variants) or consequence term \(e.g. start loss, stop gained\) from the Sequence Ontology \(SO\). If the variant maps to intergenic regions, we will assign the variant to the 5' end \(i.e. nearest likely promoter\) of the closest protein coding gene on either strand \(forward or reverse\) within a 500kb window

