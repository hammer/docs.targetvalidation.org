# How do you compute target and disease similarity?

The Similar Targets and Similar Diseases visualisations on the Target and Disease profile pages displays a list of the top 20 targets that share similar target-to-disease connections based on a systematic computation of all target-disease associations and overall association scores.

To compute the similarity between targets, we:

* Assess the overall connectivity of a target and apply a weight based on its significance and specificity
* Calculate the overlap of two targets against the total number of disease associations for each target and correct the calculation by the computed weight

The current similarity computation pipeline places an emphasis on associations with high scores \(for instance, curated rare disease associations\) and targets that are linked to few diseases \(specific\), rather than targets linked to many diseases. We also only consider target-disease pairs with at least three pieces of evidence that support the connection.

{% embed url="https://www.youtube.com/watch?v=vQXHNp-QeDw" %}



After clicking on a bubble with a similar target \(or disease\) computed by Open Targets Platform pipeline, the visualisation will display a list of up to 15 diseases used to compute the similarity score. You will also get the underlying association scores between each target and disease.

For more information on our approach to calculating related targets, please read [Open Targets Platform: new developments and updates two years on](https://europepmc.org/articles/PMC6324073).

{% hint style="success" %}
Want to access all data for the Open Targets Platform similar targets \(diseases\) analysis for a given target \(disease\)?

Use the `/private/relation/target` endpoint with the [Open Targets Platform REST API](https://docs.targetvalidation.org/programmatic-access/rest-api) .
{% endhint %}



