# Why does my search term return so many results?

When you search for a term, for example `carcinoma` or `BRCA2`, we will break it up into smaller words, according to an [Edge Ngram Tokeniser](https://www.elastic.co/guide/en/elasticsearch/reference/current/analysis-edgengram-tokenizer.html). We configure this tokeniser to treat letters \(and digits\) as tokens to produce a given choice of grams. For example, a trigram \(gram of length of three\) of `carcinoma` will give `car`, `arc`, `rci`, `cin`, `ino`, `nom`, and `oma`tokens. For the current implementation, we have chosen a four-gram tokeniser.

The search is performed across multiple fields in our in our ElasticSearch index, such as full name of a gene, approved name of a gene, approved gene symbol, description of the disease, and EFO synonyms for a disease. Each of these fields will be weigh differently: we boost the terms found under "full name" and "approved name" and down weight the terms found in the "description" or "EFO synonyms" fields. We will then apply a function based on the the number associations and finally return the results of our search in our user interface. You can then choose to refine the results by "targets' or "diseases".

This optimisation allows us to return results that were previously missed before the four-gram tokeniser implementation. In the past, when searching for Charcot-Marie-Tooth disease, for example, we would have returned no results. When searching for [Charcot-Marie-Tooth](https://www.targetvalidation.org/search?src=q:Charcot-Marie-Tooth,p:1,f:disease) and refining the results by disease, you will get the expected results.

Another advantage of the tokeniser is that you can now search for incomplete terms or names e.g. “[alzhe](https://www.targetvalidation.org/search?src=q:alzhe)” and get Alzheimer's disease in addition to other terms \(sub-types of Alzheimer's or drug targets\) related to the disease, that would return no results before implementing the tokeniser.

This is a much welcome improved on our search and autocomplete functionalities. However, a side effect of this implementation is that we now return a higher number of terms than we used to, some of them rather non-specific. If this affects your experience when using our Platform or if you want to discuss this further, please [email us](mailto:support@targetvalidation.org).

