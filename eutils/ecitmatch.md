# ECitMatch

**Base URL**
```
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/ecitmatch.cgi
```
**Function**
  * Searches PubMed for citations and retrieves PubMed IDs (PMIDs) that correspond to one or more the citation strings

 ### Required Parameters

**Table 1. ECitMatch Required Parameters**
|  Required Parameters | Common Name | Description |
| --- | --- | --- |
| db  | Database |  The database to search. The only supported value is ‘pubmed’. |
| rettype | Retrieval type | The format in which the returned information is presented. The only supported value is ‘xml’. |
| bdata | Citation strings | Citation information you provide to identify which PUbMed IDs to return |

Note:
  * Each citation string must be in the following format:<br>**journal_title|year|volume|first_page|author_name|your_key|**
    * The **your_key** value in the citration string is an arbitrary label you can provide that may serve as a local identifier for the citation. It is included in the output.
    * In the example below, the **your_key** value is _Art1_ and _Art2_
  * Multiple citation strings may be provided by separating the strings with a carriage return character ‘**%0D**’. See this in the example below.
  * All spaces must be replaced by ‘+’ symbols 
  * Citation strings should end with a final vertical bar ‘|’.

  **Example**:<br> [https://eutils.ncbi.nlm.nih.gov/entrez/eutils/ecitmatch.cgi?db=pubmed&retmode=xml&bdata=proc+natl+acad+sci+u+s+a|1991|88|3248|mann+bj|Art1|%0Dscience|1987|235|182|palmenberg+ac|Art2|](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/ecitmatch.cgi?db=pubmed&retmode=xml&bdata=proc+natl+acad+sci+u+s+a|1991|88|3248|mann+bj|Art1|%0Dscience|1987|235|182|palmenberg+ac|Art2|)
