# ACDH Assessment Task

This repository contains my solution to the assessment task for the frontend web developer position at the Austrian Centre for Digital Humanities. It includes a search view for the ACDH's MMP database implemented in vue.js.

## Quickstart

A preview of the application can be found here: https://x4ml3.csb.app/

To run the application locally, simply clone the repository and run `npm install` and `npm run serve`.

## Task completion

All of the required and proposed tasks were implemented. The developed application can easily be extended, e.g. with additional table columns by modifying the `tableCols` property of the Search module.

### Sorting according to relevance

The relevance sorting algorithm is very simple and could probably be improved by including more list-item properties. Its current version compares entries by their match of keywords with the `zitat` parameter and the number of occurrences of `zitat` in the item's text (`listItem.zitat`). Please find a pseudo code version of the comparison function below:

```
a, b ... list-items of the API's result list
z ... search term
Note: all strings operations are performed on lower case copies of the strings

// compare direct keyword matching (0 or 1)
direct_keywords_a = number of a.key_word entries that equal z;
direct_keywords_b = number of b.key_word entries that equal z;

if (direct_keywords_a == direct_keywords_b) {

    // compare keyword variant matching
    keywords_a = number of a.key_word entries of which the varianten property contains z;
    keywords_b = number of b.key_word entries of which the varianten property contains z;

    if (keywords_a == keywords_b) {

        // compare text occurrences
        text_matches_a = # of occurrences of z in a.zitat;
        text_matches_b = # of occurrences of z in b.zitat;
        return text_matches_b - text_matches_a;
    }
    else
        return keywords_b - keywords_a;
}
else
    return direct_keywords_b - direct_keywords_a;
```

### API quality

One obvious weakness of the API is the mix of languages: some properties are named in English, others in German, e.g. "summary" vs. "zitat" or "start_date" vs. "jahrhundert". This should be fixed by translating the corresponding property names to make the database accessible to non German speakers .

Another weakness is the inconsistency of entries: the value of the `autor.name` attribute is in German, whereas `ort.name` is in English. Users have to be aware of this and include the corresponding rules in their applications, in order to provide a consistent output. To better support multilingual applications, additional `author.name_de` and `ort.name_en` properties should be introduced.

Finally, the API endpoints do not return the actual `id` of an entry. Instead, the properties `legacy_id` and `legacy_pk` have to be used to obtain an item's id even though their names suggest that the attributes (and their values) may be outdated. This can be easily fixed by including an object's `id` in the response body.
