# ESpell

--> This page needs  command link example

Base URL
```
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/espell.fcgi
```

**Function**

  * Provides spelling suggestions for terms within a single text query

### Required Parameters for ESPell 

| Goal | Argument | Browser Example | Command Line Example |
| --- | ---  | --- | --- |
| Which database to search | db | db=pubmed  | -db pubmed |
| What the term(s) are you searching | term |  term=asthmaa+OR+alergies | -query "asthma [PUBMED] OR alergies [PUBMED]" |    

All special characters must be URL encoded. Spaces may be replaced by '+' signs. For very long queries (more than several hundred characters long), consider using an HTTP POST call. 

**See the PubMed or Entrez help for information about search field descriptions and tags. Search fields and tags are database specific.**



**Input**: Entrez text query (&term); Entrez database (&db)
**Output**: XML containing the original query and spelling suggestions.
  * **Example**: Find spelling suggestions for the PubMed Central query ‘fiberblast cell grwth’ <br>[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/espell.fcgi?term=fiberblast+cell+grwth&db=pmc](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/espell.fcgi?term=fiberblast+cell+grwth&db=pmc)

 * **Example**: Find spelling suggestions for the PubMed Central query 'asthmaa or alergies’ <br> [https://eutils.ncbi.nlm.nih.gov/entrez/eutils/espell.fcgi?db=pubmed&term=asthmaa+OR+alergies](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/espell.fcgi?db=pubmed&term=asthmaa+OR+alergies)
