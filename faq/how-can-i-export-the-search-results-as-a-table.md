# How can I export the search results as a table?



* You can use the Open Targets REST endpoint \`search\` to get the same results you get from the user interface: \`[https://api.opentargets.io/v3/platform/public/search?q=](https://api.opentargets.io/v3/platform/public/search?q=pulmonary&format=csv&size=211)\`

By default the \`search\` endpoint returns the results in JSON. You can add the parameters  \`&format=\` and include CSV or TAB to get the same results in a table format. Note that the endpoint returns 10 results by default. If you want to download more than 10 results, let’s say 100, you need to add \`&size=100\`.  


When searching the Platform, you will for example get 21 results in the [search results for DMD](https://www.targetvalidation.org/search?src=q:DMD) in our current release. To download these results, you will use:  


[https://api.opentargets.io/v3/platform/public/search?q=DMD&format=csv&size=21](https://api.opentargets.io/v3/platform/public/search?q=pulmonary&format=csv&size=211)  


More details on our REST API can be found in our interactive [documentation](https://api.opentargets.io/v3/platform/docs/swagger-ui).  


Please be aware that the results may change from release to release. So the same request against the 18.06 version will probably give different results from the previous release, 18.04 for example.  


