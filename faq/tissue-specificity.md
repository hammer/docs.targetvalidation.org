# What is the tissue specificity in your Platform?

We compute the tissue specificity of a target as the number of standard deviations from the mean of the log RNA expression of the target across the available tissues. This is a standard z-score calculation. A target is considered to be tissue specific if the z-score is greater than 0.674 \(or the 75th percentile of a perfect normal distribution\). We remove data for under-expressed targets before the z-score calculation. Our RNA expression data comes from Expression Atlas.

