# [![](http://www.targetvalidation.org/imgs/logo/otp-logo-w-b.svg "Open Targets logo")](http://www.targetvalidation.org/)Frequently asked questions

* [What can I search for?](http://www.targetvalidation.org/#search)
* [What is a target?](http://www.targetvalidation.org/#target)
* [How are diseases described Open Targets?](http://www.targetvalidation.org/#diseases)
* [What is the Experimental Factor Ontology?](http://www.targetvalidation.org/#efo)
* [Why does Open Targets use EFO?](http://www.targetvalidation.org/#why-efo)
* [What is the difference between direct and non-direct associations for targets and diseases?](http://www.targetvalidation.org/#direct)
* [How does Open Targets distinguish variants from mutations?](http://www.targetvalidation.org/#mutations)
* [Where does the data come from?](http://www.targetvalidation.org/#data)
* [What genome assembly does Open Targets use?](http://www.targetvalidation.org/#assembly)
* [How does Open Targets assign variants \(e.g. SNPs\) to genes?](http://www.targetvalidation.org/#variants)
* [The Open Targets Platform does not report a known association between gene A and disease Z. Why isn't this information in Open Targets?](http://www.targetvalidation.org/#missing-data)
* [What are clinical trials?](http://www.targetvalidation.org/#clinical-trials)
* [How is the association score calculated?](http://www.targetvalidation.org/#score)
* [Do you have any data on transgenic animal models?](http://www.targetvalidation.org/#transgenic)
* [I am looking at a target profile and found some articles linked to my target. Where does the bibliography come from?](http://www.targetvalidation.org/#biblio)
* [Do you use the information I have searched for in Platform?](http://www.targetvalidation.org/#data_use)
* [How do I cite the Open Targets Platform?](http://www.targetvalidation.org/#citation)
* [Can I download data from the Open Targets Platform?](http://www.targetvalidation.org/#download)
* [How can I contact the team?](http://www.targetvalidation.org/#contact)

#### What can I search for?

You can search for disease names \(e.g. Alzheimers\), gene names \(e.g. apolipoprotein E\), official gene symbols \(e.g. APOE\), Ensembl gene IDs \(e.g. ENSG00000130203\) or protein symbols \(e.g. P02649\). You may also be able to search for synonyms and abbreviations for both genes \(e.g. apolipoprotein, p94\) and diseases \(e.g. IBD\). You can also search for drugs \(e.g. ADALIMUMAB\) and phenotypes \(hyperlordosis\), which will get matched to their associated diseases and targets.

#### What is a target?

A target can be a protein, protein complex or RNA molecule. We integrate evidence to the target through the gene that codes for it. If you search for a target and cannot find it, please[email us](mailto:support@targetvalidation.org).

#### How are diseases described in Open Targets?

We map diseases to ontology terms in the Experimental Factor Ontology \(EFO\). This enables us to integrate evidence from different sources and to describe relationships between diseases.

#### What is the Experimental Factor Ontology?

The[Experimental Factor Ontology](http://www.ebi.ac.uk/efo/)\(EFO\) provides a systematic, machine readable description of data elements available in public databases. It combines parts of several ontologies, such as diseases, phenotypes, anatomy, and chemical compounds. The EFO is the core ontology for Open Targets.

#### Why does Open Targets use EFO?

These are the reasons for choosing the Experimental Factor Ontology:

* It is an application ontology, therefore it can incorporate parts \(or the whole\) of other ontologies, such as the rare disease ontology ORDO.
* It is able to bring in additional \(not disease only\) ontologies.
* It can easily accommodate our requests for new ontology terms in addition to updates and changes, as Open Targets and the EFO team collaborate closely.
* It is the ontology of controlled vocabulary used by the GWAS catalog and the Expression Atlas. Therefore, no extra step was needed when incorporating those two data sources in our pipeline.

#### What is the difference between direct and non-direct associations for targets and diseases?

We take into account the ontology of diseases from the Experimental Factor Ontology \(EFO\) to propagate evidence up to their parent terms. This allows us to compute new target-disease associations when there is no direct \(known and observed\) evidence for them. Read our[Direct versus indirect evidence: should you care?](http://blog.opentargets.org/direct-versus-indirect-evidence-should-you-care/)blog post for more details

#### Where does the data come from?

The data comes from a number of public databases, such as GWAS Catalog, EVA, UniProt, Expression Atlas, ChEMBL, DECIPHER, IntOGen, and others. These databases are the[Open Targets Platform Data Sources](http://www.targetvalidation.org/data_sources).

#### What genome assembly does Open Targets use?

We use GRCh38 \(sometimes referred to as hg38\). This is the latest human genome provided by the[Genome Reference Consortium](https://www.ncbi.nlm.nih.gov/grc). This is relevant when we display SNPs and other features on the genome. It also affects the set of targets that we use, which is based on the latest Ensembl version at the time of our release. However, because our focus is on evidence associating targets and diseases, we support most evidence data irrespective of the genome assembly that may have been used for their original analysis.

#### How does Open Targets assign variants \(e.g. SNPs\) to genes?

We map and annotate variants to genes and transcripts using the Ensembl Variant Effect Predictor \(VEP\). If a variant maps to a gene with different transcripts, we will assign it the most severe[variant definitions](http://www.targetvalidation.org/variants)or consequence term \(e.g. start loss, stop gained\) from the Sequence Ontology \(SO\). If the variant maps to intergenic regions, we will assign the variant to the 5' end \(i.e. nearest likely promoter\) of the closest protein coding gene on either strand \(forward or reverse\) within a 500kb window

#### The Platform does not report a known association between gene A and disease Z. Why isn't this information in Open Targets?

If we miss known associations that are described elsewhere, please[get in touch](mailto:support@targetvalidation.org?). The reasons can be severalfold and we will look at the examples on a case-by-case basis. If the known association is described in a recent paper, it will not have made it through the curation process within our data sources yet. If the known association is based on a variant with an ID \(e.g. rs123, His166Tyr\), please include that information as well. We are revisiting our variant-to-gene assignment to assess if eQTLs could give a more likely assignment that the one we currently use, which is based on functional data only as described in["How does Open Target assign variants \(e.g. SNPs\) to genes?"](http://www.targetvalidation.org/#variants). By providing this information, you can help us improve our analyses for variant-to-gene assignment.

#### What are clinical trials?

Clinical trials are studies carried out in human volunteers over a period of 10-15 years to investigate the safety and/or efficacy of a medicine. The Food and Drug Administration \(FDA\) describes the following phases:

* **Phase I**
  to assess the drug's most frequent \(and serious\) adverse events and how the drug is metabolised and excreted. The number of subjects \(either healthy volunteers or people with the disease/condition\) ranges from 20 to 100. Phase I takes several months.
* **Phase II**
  provides provides preliminary data on the biological activity of a drug. Safety continues to be evaluated and short-term adverse events studied. Up to 300 subjects \(volunteers with the disease/condition\) are studied. Phase II takes between several months to two years.
* **Phase III**
  continues assessing effectiveness and adverse reactions. It is carried out in 300 - 3,000 volunteers with the disease/condition from different human populations. Different dosages and the combination with other drugs can be assessed. This phase takes between one and four years
* **Phase IV**  
  occurs once the FDA authorises a drug for marketing. Further information on drug's safety, efficacy and/or optimal use will be assessed in pharmacovigilance.

  Some phase IV drugs \(e.g. from  
  [ClinicalTrials.gov](https://clinicaltrials.gov/)  
  \) may also be in postmarketing surveillance, and used for conditions different from the ones for which the drug has been originally approved for. Several thousands volunteers who have the disease/condition are studied.

This[FDA infographic](https://www.fda.gov/downloads/Drugs/ResourcesForYou/Consumers/UCM284393.pdf)gives a summary of the different phases in a clinical trial:

#### How is the association score calculated?

[Scoring target-disease associations](https://www.targetvalidation.org/scoring)is done at four levels. Firstly, we summarise the strength of the evidence. This score depends on factors that affect the relative strength of the evidence \(e.g. \*p\* values and sample size for SNPs from GWAS Catalog; or phase of the clinical trials for drugs from ChEBML\).

We then aggregate the scores from all evidence into the data source scores, followed by aggregating the data source scores into the data type scores \(e.g. Genetic associations score\). For the aggregation steps, we take into account the sum of the[harmonic progression](https://en.wikipedia.org/wiki/Harmonic_progression_%28mathematics%29), and adjust the contribution of each of them using a heuristic weighting.

Finally, we sum the individual data source scores using the harmonic sum to give the overall association score.

#### How do you calculate tissue specificity from RNA expression data?

We compute the tissue specificity of a target as the number of standard deviations from the mean of the log RNA expression of the target across the available tissues. This is a standard z-score calculation. A target is considered to be tissue specific if the z-score is greater than 0.674 \(or the 75th percentile of a perfect normal distribution\). We remove data for under-expressed targets before the z-score calculation. Our RNA expression data comes from Expression Atlas.

#### I am looking at a target profile and found some articles linked to my target. Where does the bibliography come from?

We link the gene to its protein and get the list of articles from the Publications section in[UniProt](http://www.uniprot.org/).

#### Do you use the information I have searched for in Platform?

We do not analyse the nature \(e.g disease or target names\) of any specific queries via the web interface. We use standard encryption methods \(e.g. https://\) to maintain the security of the searches. For further details check the[Terms of use for the Open Targets Platform](http://www.targetvalidation.org/terms_of_use).

Note that some of the components of the site are provided by third parties, or make use of services provided by third parties, mostly from EMBL-EBI resources. We provide links to these external resources, and the use of their services is covered by their own terms of use. We may however use some metrics on the usage of pages and icons on the platform to improve its visualisation aspects. If you any concerns, please contact our[support](mailto:support@targetvalidation.org?Subject='Open Targets Platform feedback')team

#### How do I cite the Open Targets Platform?

If you use the Open Targets Platform in your work, please cite our latest paper["Open Targets: a platform for therapeutic target identification and validation"](http://nar.oxfordjournals.org/content/early/2016/11/29/nar.gkw1055.full)

#### Can I download data from the Open Targets Platform?

Yes, you can download our data as compressed JSON files. These[file dumps are available](http://www.targetvalidation.org/downloads/data)for the target-disease association objects and the evidence objects, the latter used to calculate each association. Both association and evidence objects are also available programmatically via our API \(check our[API documentation](http://api.opentargets.io/v3/platform/docs)\).

#### How does Open Targets distinguish variants from mutations?

Variants are base differences observed in the human population \(e.g. 1000 Genomes, ExAC data\), whereas mutations are base changes that have been associated with a significant phenotypic change. Changes associated with a rare disease or cancer are referred as mutations.

#### Do you have any data on transgenic animal models?

We have the knockout models from the[Mouse Genome Informatics](http://www.informatics.jax.org/)., not the transgenic ones. If you want the transgenic data to be incorporated as well, please[email us](mailto:support@targetvalidation.org).

#### How can I contact the team?

If you have questions or feedback,[email us](mailto:support@targetvalidation.org). You can also follow the team and keep up with the latest news on Open Targets and its Open Targets Platform through our social media channels[Twitter](https://twitter.com/targetvalidate),[Facebook](https://www.facebook.com/OpenTargets)and[LinkedIn](https://www.facebook.com/OpenTargets).

#### 



