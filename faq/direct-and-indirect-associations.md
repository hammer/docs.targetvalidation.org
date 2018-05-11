# Direct and indirect associations

We take into account the ontology of diseases from the Experimental Factor Ontology \(EFO\) to propagate evidence up to their parent terms. This allows us to compute new target-disease associations when there is no direct \(known and observed\) evidence for them. Read our [Direct versus indirect evidence: should you care?](http://blog.opentargets.org/direct-versus-indirect-evidence-should-you-care/) blog post for more details

When using our web interface, you will get associations based on direct evidence only \(if searching for a target\), or both direct and indirect associations \(if searching for a disease\).

For instance, IBD is a child of autoimmune disease, and the parent term of other related diseases, such as [ulcerative colitis](http://www.targetvalidation.org/disease/EFO_0000729) and [Crohn's disease](http://www.targetvalidation.org/disease/EFO_0000384).

.![](../.gitbook/assets/ibd-efo-tree.png)

We use these parent-child relationships to propagate direct evidence from IBD up to higher levels in its ontology tree, and to provide additional integration. We refer to this type of evidence as indirect. We use indirect evidence to expand the number of associations that we would not have identified otherwise.

What does this expansion based on indirect evidence enable us to do?

* it allows finding common targets across groups of related diseases \(e.g. ulcerative colitis, Crohn's disease and inflammatory bowel disease\).
* it makes connections between rare and common diseases \(e.g. autosomal recessive early-onset inflammatory bowel disease and inflammatory bowel disease\).
* it groups evidence for all diseases within a therapeutic area.
* it allows the identification of unforeseen associations by serendipity.

Moreover, the different evidence types coming from our [data sources](https://www.targetvalidation.org/data_sources) often are associated with diseases at different levels of their ontology. For instance, the electronic description of diseases from drugs in clinical trials can be quite general, whereas rare genetic diseases are defined in much greater detail.

When you search for\_IL10RA\_using the web interface, you will find all [diseases associated with IL10RA](https://www.targetvalidation.org/target/ENSG00000110324/associations).

![](../.gitbook/assets/il10ra.png)

If you use our`/public/search`[endpoint](http://targetvalidation.org/api/latest/public/search?q=ENSG00000110324), you will see two types of association counts:

* total:

  `n=178`

* direct:

  `n=97`

```javascript

```

The difference between`total`and`direct`is the number of associations based on indirect evidence \(`n=81`\).

We do not display the indirect associations in the web interface.

But you can get all the 81 diseases associated with\_IL10RA\_through indirect evidence with the`/association/filter`[endpoint](http://www.targetvalidation.org/api/latest/public/association/filter?target=ENSG00000110324&direct=false&fields=is_direct&fields=disease.efo_info.label&size=100). Make sure you include the`direct=false`,`fields=disease.efo_info.label`and`size=100`parameters.

On the web interface, When starting with a disease, you will get both direct and indirect associations.

We have [4553 targets associated with inflammatory bowel disease](https://www.targetvalidation.org/disease/EFO_0003767/associations). If you use our`/public/search`[endpoint](http://targetvalidation.org/api/latest/public/search?q=EFO_0003767), you will see`n=4553`and`n=2276`for the total and direct number of association counts, respectively.

\`\`\`json

```text

```

The remainder \(`n=2277`\) are the targets associated with IBD using the indirect evidence coming from child terms of IBD, e.g. ulcerative Colitis or Crohn's Disease.

You can customise the API call with the`direct=false`parameter if you rather focus on indirect associations instead. Make sure you adjust the field`size=`so that you include all 2277 targets.

If you want to pick and choose which associations to focus on, use our [REST API](https://www.targetvalidation.org/documentation/api). It will allow you to customise your queries with greater flexibility than using the web interface.

