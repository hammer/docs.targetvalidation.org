# How can I export the search results?

When searching for a term using the Open Targets Platform graphical interface, you may want to download the results you get. Although we do not provide a download option straight from the user interface, you can easily retrieve the same results using the Open Targets [REST API](https://docs.targetvalidation.org/programmatic-access/rest-api). 

Let's take the target DMD, for example. When you search for DMD, you get 23 results, which can be refined by target \(21 entries\) or disease \(2 entries\) for targets \(these numbers are for release 19.09 and may vary from release to release\).

Use the `search` endpoint to returns the same results in JSON:

{% embed url="https://platform-api.opentargets.io/v3/platform/public/search?q=dmd" %}

Alternatively, you can use `curl`:

```text
curl -X GET "https://platform-api.opentargets.io/v3/platform/public/search?q=dmd" -H "accept: application/json"
```

If you rather have the results in a table format, add the parameter `&format=` and include CSV or TAB. Note that the `search` endpoint returns 10 results by default. If you want to download all the results for DMD, you need to add `&size=23`.

{% embed url="https://api.opentargets.io/v3/platform/public/search?q=DMD&format=csv&size=23" %}

  


