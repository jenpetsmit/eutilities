# ESummary

**Base URL**

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi```

**Functions**

  * Returns document summaries (DocSums) for a list of input UIDs
  * Returns DocSums for a set of UIDs stored on the Entrez History server  **(Noteto self:  Add Link to History Server)**

**Table: Required Fields for ESummary**    

| Goal | Argument | Browser Example | Command Line Example |
| --- | ---  | --- | --- |
| Which database to search | db | db=nucore  | -db nucore |
| Which UIDs to include | id | id= |

**Optional Fields for ESummary**  

**retstart**

  * Sequential index of the first DocSum to be retrieved (default=1, corresponding to the first record of the entire set). This parameter can be used in conjunction with retmax to download an arbitrary subset of DocSums from the input set.

**retmax**

  * Total number of DocSums from the input set to be retrieved, up to a maximum of 10,000. If the total set is larger than this maximum, the value of retstart can be iterated while holding retmax constant, thereby downloading the entire set in batches of size retmax.

**retmode**

  * Retrieval type. Determines the format of the returned output. The default value is ‘xml’ for ESummary XML, but ‘json’ is also supported to return output in JSON format.

**version**

  * Used to specify version 2.0 ESummary XML. The only supported value is ‘2.0’. When present, ESummary will return version 2.0 DocSum XML that is unique to each Entrez database and that often contains more data than the default DocSum XML.

 
## Ouput
  * Provides a list of  UIDs matching a text query
  * Posts the results of a search on the History server
  * Downloads all UIDs from a dataset stored on the History server 
  * Combines or limits UID datasets stored on the History server
  * Sorts sets of UIDs

 # Example
 
Download nuccore GIs 34577062 and 24475906 in FASTA format
```
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nuccore&id=34577062,24475906&rettype=fasta 
```
 
