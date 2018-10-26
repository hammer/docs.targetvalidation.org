# What is an indirect association?

We take into account the ontology of diseases from the Experimental Factor Ontology \(EFO\) to propagate evidence up to their parent terms. This allows us to compute new target-disease associations when there is no direct \(known and observed\) evidence for them. When using evidence propagated in the ontology, the association is an indirect association.

If you use the web interface of our Platform, you will get associations based on direct evidence only if searching for a **target**. ****If you searching for a disease, you will get  both direct and indirect associations.

If you retrieve our target-disease associations via the REST-API, you will get two types of association counts:

* total:

  `n=178`

* direct:

  `n=97`

The difference between`total`and`direct`is the number of associations based on indirect evidence. If you want the associations based on direct evidence only, you should use `direct = true`parameter.

Read our [Direct versus indirect evidence: should you care?](http://blog.opentargets.org/direct-versus-indirect-evidence-should-you-care/) blog post for more details



