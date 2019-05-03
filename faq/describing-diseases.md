# How do you describe diseases?

We use a slimmed version of the Experimental Factor Ontology \(EFO\) to describe diseases available in the Open Targets Platform. This modified ontology consists of a subset of EFO terms in addition to terms from other ontologies \(e.g. Human Phenotype Ontology - HPO\) for which an EFO term is not available.

We map diseases to our Open Targets Platform ontology using [OnToma](https://ontoma.readthedocs.io/en/stable/) to integrate evidence from different sources and describe relationships between diseases.

The reasons for choosing EFO as our core ontology are listed below:

* It is an application ontology, therefore it can incorporate parts \(or the whole\) of other ontologies, such as the rare disease ontology ORDO
* It is able to bring in additional \(not disease only\) ontologies
* It can easily accommodate our requests for new ontology terms in addition to updates and changes, as Open Targets and the EFO team collaborate closely
* It is the ontology of controlled vocabulary used by the GWAS catalog and the Expression Atlas. Therefore, no extra step was needed when incorporating those two data sources in our pipeline

