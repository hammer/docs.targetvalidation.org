# What is an indirect association?

Indirect associations between targets and diseases are computed based on indirect evidence, rather than direct, observed evidence. They can be retrieved using both the Open Targets Platform user interface and the REST-API.

If you search for a **target** using the web interface, you will get associations based on direct evidence only However, ****if you search for a disease, you will get both direct and indirect associations.

When using the If you use our target-disease associations via the REST-API, you will get two types of association counts:

![Association counts when searching for Alzheirmer&apos;s using the REST-API \`search\` endpoint](../.gitbook/assets/screen-shot-2018-10-26-at-10.17.43.png)

* total:

  `n=3214`

* direct:

  `n=3110`

The difference between`total`and`direct`is the number of indirect associations based on indirect evidence. 

We propagate the indirect evidence from a child disease term up to their parent terms in any ontology of our diseases. By computing new target-disease associations when there is no direct \(known and observed\) evidence for them, we allow:

* finding common targets across groups of related diseases \(e.g. ulcerative colitis, Crohn's disease and inflammatory bowel disease\)
* making connections between rare and common diseases \(e.g. autosomal recessive early-onset inflammatory bowel disease and inflammatory bowel disease\)
* grouping evidence for all diseases within a therapeutic area
* identifying unforeseen associations by serendipity

 



. When using evidence propagated in the ontology, the association is an indirect association.

Read our [Direct versus indirect evidence: should you care?](http://blog.opentargets.org/direct-versus-indirect-evidence-should-you-care/) blog post for more details



