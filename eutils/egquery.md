# EGQuery

**Base URL**

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/egquery.fcgi```

**Function**

Searches a text query in all Entrez databases and returns the number of results for the query in each database.

## Required Parameter
 ### Required Parameters

**Table 1. EGQuery Required Parameters**
 |  Required Parameters | Common Name | Description |
 | --- | --- | --- |
 | term  | term |  Entrez text query |
 
  * [All special characters must be URL encoded](https://github.com/jenpetsmit/eutilities/blob/main/access/browser.md#rules-of-writing-entrez-api-urls).
  * Replace spaces with '+' signs.
    *  For very long queries (more than several hundred characters long), consider using an HTTP POST call.
    *  See the PubMed or Entrez help for information about search field descriptions and tags. Search fields and tags are database specific.

### Example

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/egquery.fcgi?term=asthma](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/egquery.fcgi?term=asthma)

 
