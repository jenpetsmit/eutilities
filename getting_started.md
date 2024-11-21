# Getting Started with E-utilities

Entrez Utilities (E-Utilities) is an Application Program Interface (API) that helps you gather data from most of the 40 NCBI Entrez database residing at the NCBI using queries. The databases include a variety of biomedical data, including nucleotide and protein sequences, gene records, three-dimensional molecular structures, and the biomedical literature.  The E-Utilities give you control over what fields to search, the data to retrieve, the data format, and how to share results. 

Figure: The Relationship between the User and NCBI Databases with the list of E-utilites as the Interface

![Figure showing the relationship between the User and NCBI databases with the list of E-utilites as the Interface](eutilies/images/about/relateFig1.png)

Users can interact with the E-Utility APIs via the following options. Click a link to jump to that page. **MOVE THIS**
  * [Internet Browser](./access/browser.md)
  * [Commmand Line](./access/commandline.md)
  * [Programmatically](./access/programmatically.md)

## API URL

Entrez API queries have three parts:
 * Base URL
 * E-Utility
 * Parameters

## Building a Simple Entrez Query

 1. Start all Entrez queries with the following base URL:
 
```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/{   }.fcgi?```

 2.	Add an _**E-Utility**_ plus “**.fcgi?**”

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/**E-Utility.fcgi?**```

  * See Table 1 for a list of E-Utilities with descriptions

 3.	Add required and optional parameters
   
```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/E_Utilitiy.fcgi?**parameters**```

  * See Table 2 for a list of parameters with descriptions

Here is an example of a simple Entrez query. You can click or copy and paste the URL in an internet browser to see how browser-based access works:
```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?db=pubmed&id=19393038```

  

### E-Utilities
The Entrez API includes nine E-Utilities. In Table 1, see the list of E-Utilities with a short description.  
Each E-Utility name is linked to its own page with complete information.  

Replace the brackets with one of the nine E-utilities listed below. For detailed information about each E-utility, click on the name.
| E-Utility   | Brief Description | 
| --- | --- |
|   [einfo](./eutils/einfo.md)   |  Retrieves information and statistics about a single database <br>  If no database is provide, einfo returns the list of current databases in the Entrez network. |
|  [esearch](./eutils/esearch.md)    | Returns a list of UIDs from a single database containing the searched text    |
|  [egquery](./eutils/egquery.md)     |  Searches a text query in all Entrez databases and returns the number of results [IN THE FORM OF UID PERHAPS?]   in each database   |
|    [efetch](./eutils/efetch) | Returns a full data record  [ DEFINE “FULL RECORD”]    |
|   [esummary](./eutils/esummary.md)  	  |  Downloads document summaries for each UID   |
| [elink](./eutils/elink.md)     |  Retrieves UIDs for related or linked records, or LinkOut URLs  [WHAT IS A LINKOUT URL?]   |
| [espell](./eutils/espell.md)     |  	Retrieves spelling suggestions for a text query […FOR WHEN YOU DON’T KNOW HOW TO SPELL SOMETHING?]   |
|  [ecitmatch](./eutils/ecitmatch.md)  	  |  Searches PubMed for a series of citation strings   [DEFINE CITATION STRING]   |
|   	[epost](./eutils/epost.md)   |  Saves a list of UIDs you can use subsequently with other E-Utilities like esummary or efetch   |
   

## E-Utilities Paremeters
Parameters are options you add to the base URL and E-Utility to limit the results.  Each E-Utility has required and optional parameters. Null values or inappropriate parameters are generally ignored
See Table 2 for a list of the most often used parameters.   For a full list, see E-Utilities Parameters page to see the required and optional parameter options for each E-Utility.

**Table 2:** Most Often Used Parameters [THIS PROBABALY NEEDS MORE WORK] 

| Common name      | Works with          | What does it do?         | Example             | Notes     |
| --- | ---  | ---  | ---  | ---  |
| Database | einfo<br> esearch<br> esummary<br> epost<br> elink<br> espell<br> ecitmatch<br>efetch  | Limits results to the provided database | db=<entrez database query name>   | db=gap  |  
| Term    | egquery<br> esearch<br> elink<br> espell        | Includes the term you provide in the query     | term=<text>     | term=asthma     |
| UID list      | esummary<br>epost<br> elink<br> efetch       | Limits results to the provided UIDs    | id=<UID>     | id=19393038,30242208,29453458      |
| Use History      | esearch      | Use history flag            | usehistory=y         |    EXAMPLE                   |
| Return max      | esearch<br>esummary         | Total number of DocSums from the input set to be retrieved, up to a maximum of 10,000 | retmax=<maximum number of results you want>      | retmax=10       |
| Retrieval mode   | esummary<br> einfo<br> esearch<br> efetch<br> elink     | Formats of the output       | retmode=json, retmode=xml      | XML is the default<BR> all E-Utilities support JSON except efetch  |
| Relative Date       | esearch       | Sets the days to be searched relative to the current date   | reldate         |  EXAMPLE      |
| Minimum Date and Maximum Date | esearch<br> elink       | Specifies the date according to the format YYYY/MM/DD<br> YYYY<br> or YYYY/MM | mindate and maxdate    | A query must contain both mindate and maxdate parameters    |
| Retrieval Type     | ecitmatch<br> efetch<br> einfo<br> elink<br> esummary<br> esearch    | rettype     |   EXAMPLE   | Return types vary by E-Utility     |


#### Common Parameters

**UID**
The UID is a unique identifier (UID) used to identify a record in an NCBI database. The combination of the database alias and UID DOES SOMETHING?
E-utility alias -id

**database parameter**
The most common parameter is db, which narrows the search to one database.
example: db=pubmed
E-utility alias - db

See [Database Parameters](eutils/database_parameters.md) for list of databases, descriptions, and other parameters that partner with the database parameter



**Response Parameters**
  * **rettype** | The type of information to return
  * **retmode** | The format of the response. XML (default) and JSON are the two options
  * **remax** | The maximum number of records returned. The default number is 20. The maximum number is 10,000
  * **retstart** | when a query returns a response and each response is assigned to an index,  use retstart to indicate the index number of the first record   [NOT SURE THIS IS RIGHT]




**Data parameters**
  * **pdat**  | publication data
  * **reldate**  | days to be search relative to the current date.  reldate =1 is for the most recent date
  * **mindate** and **maxdate** are used togeteher to provide a date range. mindate=YYY/MM/DD or YYYY/MM&maxdate=YYYY/MM/DD or YYYY/MM
  * **cmd** | may  not belong in this list. relevant to elink and used to inidcate whether or not to return IDs of simliar artcles or URSL to full text [IS THIS STILL TRUE?]
