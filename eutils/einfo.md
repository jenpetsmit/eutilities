# EInfo



the information copied below from this page:
[https://www.ncbi.nlm.nih.gov/books/NBK25499/#_chapter4_EInfo_](https://www.ncbi.nlm.nih.gov/books/NBK25499/#_chapter4_EInfo_)


## Base URL
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/einfo.fcgi

## Functions
  * Provides a list of the names of all valid Entrez databases if no database is provided
  * Provides statistics for a single database, including lists of indexing fields and available link names when a database is provided

### Required Parameters for EInfo 
There are no required parameters. If no db parameter is provided, EInfo will return a list of the names of all valid Entrez databases.

### Optional Parameters for EInfo

|  Optional Parameters | Common Name | Description |
| --- | --- | --- |
| db  | Database |  The database about which to gather statistics |
| version | version | Used to specify version 2.0 EInfo XML. The only supported value is ‘2.0’. <br>When present, EInfo will return XML that includes two new fields: {IsTruncatabl} and {<IsRangeable}. <br>  * Fields that are able to be truncated allow the wildcard character ‘*’ in terms. The wildcard character will expand to match any set of characters up to a limit of 600 unique expansions.  <br>  *  Fields that are able to use a range allow the range operator ‘:’ to be placed between a lower and upper limit for the desired range (e.g. 2008:2010[pdat]). |
| retmode | Retrieval type | Determines the format of the returned output. The default value is ‘xml’.Also‘json’ is supported. |


## Examples
  * Return a list of all Entrez database names: <br>[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/einfo.fcgi](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/einfo.fcgi)

  * Return version 2.0 statistics for Entrez Protein: <br> [https://eutils.ncbi.nlm.nih.gov/entrez/eutils/einfo.fcgi?db=protein&version=2.0](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/einfo.fcgi?db=protein&version=2.0)
  * Return version 2.0 statistics for Entrez Protein in json format: <br> [https://eutils.ncbi.nlm.nih.gov/entrez/eutils/einfo.fcgi?db=protein&version=2.0&retmode=json](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/einfo.fcgi?db=protein&version=2.0&retmode=json)
