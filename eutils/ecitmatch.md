# ECitMatch

**Base URL**
```
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/ecitmatch.cgi
```
**Function**
  * Retrieves PubMed IDs (PMIDs) that correspond to a set of input citation strings.      

**Required Parameters**

**db**
  * Database to search. The only supported value is ‘pubmed’.

**rettype**
  * Retrieval type. The only supported value is ‘xml’.

**bdata**
  * Citation strings. Each input citation must be represented by a citation string in the following format:<br>**journal_title|year|volume|first_page|author_name|your_key|**
  * Multiple citation strings may be provided by separating the strings with a carriage return character ‘**%0D**’.
  * The **your_key** value is an arbitrary label you provide that may serve as a local identifier for the citation. It is included in the output.
  * All spaces must be replaced by ‘+’ symbols 
  * Citation strings should end with a final vertical bar ‘|’.

  **Example**:<br> [https://eutils.ncbi.nlm.nih.gov/entrez/eutils/ecitmatch.cgi?db=pubmed&retmode=xml&bdata=proc+natl+acad+sci+u+s+a|1991|88|3248|mann+bj|Art1|%0Dscience|1987|235|182|palmenberg+ac|Art2|](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/ecitmatch.cgi?db=pubmed&retmode=xml&bdata=proc+natl+acad+sci+u+s+a|1991|88|3248|mann+bj|Art1|%0Dscience|1987|235|182|palmenberg+ac|Art2|)
