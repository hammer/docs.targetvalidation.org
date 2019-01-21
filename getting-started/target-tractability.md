# Target tractability

The assessment of target tractability allows you to exploit target details, such as whether there is a binding site in the protein that can be used for small molecule binding, or an accessible epitope for antibody based therapy. This can assist in target prioritisation, drug target inclusion in discovery pipelines and selection of therapeutic modalities that are most likely to succeed.

Another advantage of tractability data is that it allows you to exploit targets for which there are no ligands or experimental structure, or those targets which are outside a "druggable" target family, but which have strong genetic associations.

{% hint style="info" %}
Check our FAQs for our definition of [target tractability](https://docs.targetvalidation.org/faq/what-is-target-tractability).
{% endhint %}

Our target tractability is based on a modified version of [Approaches to target tractability assessment – a practical perspective](https://pubs.rsc.org/en/content/articlelanding/2018/md/c7md00633k#!divAbstract). We have been working with our partners to evaluate and validate existing tractability methods. The data that is available in our Open Targets Platform is the first step of this project: _in silico_ tractability assessment pipeline of 20,633 targets for small molecules and antibodies.

Each of these targets is described following a hierarchical qualitative buckets of tractability based on data from UniProt, HPA, PDBe, DrugEBIlity, ChEMBL, Pfam, InterPro, Complex Portal, DrugBank, Gene Ontology, and BioModels. 

| Buckets | Small molecule                                             | Monoclonal antibody |
| :--- | :--- | :--- |
| 1 | Targets with drugs in phase IV | Targets with drugs in phase IV |
| 2 | Targets with drugs in phase II or above | Targets with drugs in phase II or above |
| 3 | Pre-clinical targets | Preclinical targets |
| 4 | Targets with crystal structures with ligands  | Targets located in the plasma membrane  |
| 5 | Targets with a drugEBIlity score equal or greater than 0.7 | Targets with GO cell component terms plasma membrane or secreted |
| 6 | Targets with drugEBIlity between zero and 0.7 | Targets with GO cell component terms plasma membrane or secreted with low or unknown confidence |
| 7 | Targets with ligands | Targets with predicted signal peptide and transmembrane domains |
| 8 | Targets with a predicted Ro5 druggable domain \(druggable genome\) | GO cell component - medium confidence |
| 9 | N.A. | Human Protein Atlas - high confidence |

When you search for a disease, you will find the list of target associated with that disease. By default, the table shows the `Associations view`. We now provide an additional view called `Prioritisation view`, where you will see some key target attributes, such as tractability information, in addition to target to disease association evidence. This is what you will find when searching for the [targets associated with Alzheimer's](https://www.targetvalidation.org/disease/EFO_0000249/associations) and click on the "Prioritisation view":

![](../.gitbook/assets/screen-shot-2018-11-23-at-17.09.13.png)

For any of those targets, we will highlight whether small molecule or antibody have been predicted to tract the target. Click on any of the cells coloured in light purple to get redirected to the target profile page. 

In the profile page of a target, such as [PSEN1](https://www.targetvalidation.org/target/ENSG00000080815?view=sec:tractability), you will see the following:

![](../.gitbook/assets/screencapture-targetvalidation-org-target-ensg00000080815-2018-11-23-17_14_27.png)

In `Target tractability`, you will see three different categories corresponding to the buckets 1-9 listed above. The correspondence between the bucket numbers and the precedence/tractable categories are listed below:

* A\) small molecule: 

  * clinical precedence: buckets 1, 2 and 3
  * discovery precedence: buckets 4 and 7
  * predictable tractable: buckets 5, 6 and 8

* B\) antibody:
  * clinical precedence: buckets 1, 2 and 3
  * predictable tractable - high confidence: buckets 4 and 5
  * predictable tractable - medium to low confidence: buckets 6, 7, 8 and 9



{% hint style="info" %}
Want to retrieve target tractability data with the [Open Targets REST API](https://api.opentargets.io/v3/platform/docs/swagger-ui)? 

Use our`private/target` endpoint:

```
curl -X GET https://api.opentargets.io/v3/platform/private/target/ENSG00000000938
```
{% endhint %}

{% hint style="danger" %}
Please be aware that the above endpoint is part of our`private` methods. `Private` methods are subject to change without prior notice, therefore they are not stable and you should use them at your own risk.
{% endhint %}

