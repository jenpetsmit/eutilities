# ESearch

Finds text in a single NCBI database


**esearch.fcgi?db=<database>&term=<query>**

**Table: Required Fields for ESearch**    

| Goal | Argument | Browser Example | Command Line Example |
| --- | ---  | --- | --- |
| Which database to search | db | db=nucore  | -db nucore |
| What the term(s) are you searching | -query | -query "insulin [PROT] AND rodents [ORGN]" |

**Table: Useful Optional Fields for ESearch**  

 | common name | Argument |  Browser Example | Command Line Example |
| --- | ---  | --- | --- |
| Maximum number of Returned Records | retmax | retmax=nucore |-retmax nucore
| other paramter | arugment | arugment= abc | -aurgment   |
 
 
## Ouput
  * Provides a list of  UIDs matching a text query
  * Posts the results of a search on the History server
  * Downloads all UIDs from a dataset stored on the History server 
  * Combines or limits UID datasets stored on the History server
  * Sorts sets of UIDs

# edit this section below

examples and text from here: https://www.ncbi.nlm.nih.gov/books/NBK25500/#chapter1.Searching_a_Database

## Storing Search Results Example
esearch.fcgi?db=<database>&term=<query>&usehistory=y
Input: Any Entrez text query (&term); Entrez database (&db); &usehistory=y
Output: Web environment (&WebEnv) and query key (&query_key) parameters specifying the location on the Entrez history server of the list of UIDs matching the Entrez query
Example: Get the PubMed IDs (PMIDs) for articles about breast cancer published in Science in 2008, and store them on the Entrez history server for later use
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&term=science[journal]+AND+breast+cancer+AND+2008[pdat]&usehistory=y

### Associating Search Results with Existing Search Results
esearch.fcgi?db=<database>&term=<query1>&usehistory=y
# esearch produces WebEnv value ($web1) and QueryKey value ($key1) 
esearch.fcgi?db=<database>&term=<query2>&usehistory=y&WebEnv=$web1
# esearch produces WebEnv value ($web2) that contains the results of both searches ($key1 and $key2)

Input: Any Entrez text query (&term); Entrez database (&db); &usehistory=y; Existing web environment (&WebEnv) from a prior E-utility call
Output: Web environment (&WebEnv) and query key (&query_key) parameters specifying the location on the Entrez history server of the list of UIDs matching the Entrez query
