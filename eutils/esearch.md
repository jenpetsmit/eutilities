# ESearch

Finds text in a single NCBI database


**esearch.fcgi?db=<database>&term=<query>**

 ### Required Fields for ESearch 

| Goal | Argument | Browser Example | Command Line Example |
| --- | ---  | --- | --- |
| Which database to search | db | db=nucore  | -db nucore |
| What the term(s) are you searching | term=insulin&rodents | -query "insulin [PROT] AND rodents [ORGN]" |

### Optional Parameters - Using the History Server
The parameters usehistory, WebEnv, and query_key work together in a series of queries. Search results are saved to the History server. Web Environment is a string from a previous search that is reused in the subsequent query.Query Key finds where the previous search and the new search overlap so that previous search results can be combined or limited.

 |  Goal | Argument |  Browser Example | Command Line Example |
| --- | ---  | --- | --- |
| Save results to or search from _History Server_ to use on subsequent queries | &usehistory=y | &usehistory=y |  |
 | Query using history results saved to _Web Environment_ | &WebEnv | &WebEnv=<webenv string> |     |
 | Find the intersection of the set specified by query_key and the set retrieved by the query in term (i.e. joins the two with AND) | query+key= |       | 

 **Note**: While only one query_key parameter can be provided to ESearch, any number of query keys can be combined in **term**. If query keys are provided in **term**, they can be combined with **OR** or **NOT** in addition to **AND**.

#### For all other optional parameters see the following:
  * [Retrival Parameters](parameters.md#retrival-parameters)
  * [Date Parameters](parameters.md#date-parameters)
 
## Functions
  * Provides a list of  UIDs matching a text query
  * Posts the results of a search on the History server
  * Downloads all UIDs from a dataset stored on the History server 
  * Combines or limits UID datasets stored on the History server
  * Sorts sets of UIDs

### PubMed Specifics
API users should be aware that some NCBI products contain search tools that generate content from searches on the web interface that are not available to ESearch. For example, the PubMed web interface (pubmed.ncbi.nlm.nih.gov) contains citation matching and spelling correction tools that are only available through that interface. Please see ECitMatch and ESpell below for API equivalents.

PubMed also offers “proximity searching” for multiple terms appearing in any order within a specified number of words from one another in the [Title] or [Title/Abstract] fields. For example:
```
esearch.fcgi?db=pubmed&term=”asthma treatment”[Title:~3]
```
# edit this section below

examples and text from here: https://www.ncbi.nlm.nih.gov/books/NBK25500/#chapter1.Searching_a_Database

## Storing Search Results Example
 
esearch.fcgi?db=<database>&term=<query>&usehistory=y

Input: Entrez text query (&term); Entrez database (&db); &usehistory=y

Output: Web environment (&WebEnv) and query key (&query_key) parameters specifying the location on the Entrez history server of the list of UIDs matching the Entrez query

Example: Get the PubMed IDs (PMIDs) for articles about breast cancer published in Science in 2008, and store them on the Entrez history server for later use
```
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&term=science[journal]+AND+breast+cancer+AND+2008[pdat]&usehistory=y

term=insulin&rodents
```
### Associating Search Results with Existing Search Results

esearch.fcgi?db=<database>&term=<query1>&usehistory=y

# esearch produces WebEnv value ($web1) and QueryKey value ($key1)

esearch.fcgi?db=<database>&term=<query2>&usehistory=y&WebEnv=$web1

# esearch produces WebEnv value ($web2) that contains the results of both searches ($key1 and $key2)

**Input**: Any Entrez text query (&term); Entrez database (&db); &usehistory=y; Existing web environment (&WebEnv) from a prior E-utility call

**Output**: Web environment (&WebEnv) and query key (&query_key) parameters specifying the location on the Entrez history server of the list of UIDs matching the Entrez query
