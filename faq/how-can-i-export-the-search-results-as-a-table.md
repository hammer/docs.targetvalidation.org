# How can I export the search results?

When searching for a term using the Open Targets Platform graphical interface, you may want to download the results you get. Although we do not provide a download option straight from the user interface, you can easily retrieve the same results using our Open Targets REST-API. 

Let's take the target DMD, for example. When you searching for DMD, you get 20 results from our 18.08 release.

You can use the `search` endpoint to returns the same results in JSON:

If you rather have the results in a table format, simply add the parameter `&format=` and include CSV or TAB. Note that the `search` endpoint returns 10 results by default. If you want to download all the results for DMD, you need to add `&size=20`.

[https://api.opentargets.io/v3/platform/public/search?q=DMD&format=csv&size=20](https://api.opentargets.io/v3/platform/public/search?q=DMD&format=csv&size=20)

More details on our REST API can be found in our  [documentation](https://api.opentargets.io/v3/platform/docs/swagger-ui).

  


