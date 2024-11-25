# EGQuery

**Base URL**

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/egquery.fcgi```

**Function**

Searches a text query in all Entrez databases and returns the number of results for the query in each database.

## Required Parameter
**term**

**Entrez text query.** All special characters must be URL encoded. Spaces may be replaced by '+' signs. For very long queries (more than several hundred characters long), consider using an HTTP POST call. See the PubMed or Entrez help for information about search field descriptions and tags. Search fields and tags are database specific.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/egquery.fcgi?term=asthma](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/egquery.fcgi?term=asthma)

 
