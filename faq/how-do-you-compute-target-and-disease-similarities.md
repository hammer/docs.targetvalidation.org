# How do you compute target and disease similarities?

The `Similar targets (based on diseases in common)` visualisation displays a list of the top 20 targets that share similar target-to-disease connections based on a systematic computation of all target-disease associations and the overall [association score](https://docs.targetvalidation.org/getting-started/scoring).

To compute the similarity between targets, we:

1\) Assess the overall connectivity of a target and apply a weight based on its significance and specificity; and

2\) Calculate the overlap of two targets against the total number of disease associations for each target and correct the calculation by the computed weight.

The current similarity computation pipeline places an emphasis on associations with high scores \(for instance, curated rare disease associations\) and targets that are linked to few diseases \(specific\), rather than targets linked to many diseases. We also only consider target-disease pairs with at least three pieces of evidence that support the connection. 

{% embed url="https://www.youtube.com/watch?v=vQXHNp-QeDw" %}

After clicking on a bubble with a similar target computed by our pipeline, the visualisation will display a list of up to 15 diseases used to compute the similarity score and the underlying association scores between each target and disease.

To access all of the data from the `similar targets` analysis, you can use the private endpoint [relation/target/](https://platform-api.opentargets.io/v3/platform/docs/swagger-ui#/private/getRelationByENSGID) from the Open Targets [REST API](https://docs.targetvalidation.org/programmatic-access/rest-api), followed by the Ensembl gene ID for your target e.g. [ENSG00000145335](https://platform-api.opentargets.io/v3/platform/private/relation/target/ENSG00000145335) for SNCA.

{% hint style="info" %}
Note that a similar visualisation is available in the disease profile page, under `Similar diseases (based on targets in common).` 

The REST API endpoint for similar diseases based on targets in common is `relation/disease` followed by the disease ID e.g. [Orphanet\_411602](https://platform-api.opentargets.io/v3/platform/private/relation/disease/Orphanet_411602).
{% endhint %}

For more information on the approach to calculating related targets \(and diseases\), please read [Open Targets Platform: new developments and updates two years on](https://europepmc.org/articles/PMC6324073).

