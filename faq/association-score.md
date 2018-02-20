#### How is the association score calculated?

[Scoring target-disease associations](https://www.targetvalidation.org/scoring) is done at four levels. Firstly, we summarise the strength of the evidence. This score depends on factors that affect the relative strength of the evidence \(e.g. \*p\* values and sample size for SNPs from GWAS Catalog; or phase of the clinical trials for drugs from ChEBML\).

We then aggregate the scores from all evidence into the data source scores, followed by aggregating the data source scores into the data type scores \(e.g. Genetic associations score\). For the aggregation steps, we take into account the sum of the [harmonic progression](https://en.wikipedia.org/wiki/Harmonic_progression_%28mathematics%29), and adjust the contribution of each of them using a heuristic weighting.

Finally, we sum the individual data source scores using the harmonic sum to give the overall association score.

