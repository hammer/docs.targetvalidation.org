# How do you score the associations?

We score target-disease associations across four different tiers.

Firstly, we summarise the strength of the evidence. This score depends on factors that affect the relative strength of the evidence \(e.g. \*p\* values, sample size and consequence terms for SNPs from GWAS and PheWAS resources; or the phase of clinical trials for drugs from ChEBML\).

We then aggregate the scores from all evidence into the data source scores \(e.g. Gene2Phenotype, PheWAS catalog\), followed by aggregating data source scores into data type scores \(e.g. Genetic associations score\). For the aggregation steps, we take into account the sum of the [harmonic progression](https://en.wikipedia.org/wiki/Harmonic_progression_%28mathematics%29), and adjust the contribution of each of them using a heuristic weighting.

Finally, we sum individual data source scores using the harmonic sum to give the overall [association score](https://docs.targetvalidation.org/getting-started/scoring).

