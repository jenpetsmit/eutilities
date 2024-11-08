# About E-utilities

For latest announcments, please visit the E-Utilities News page.

NCBI Entrez utilities (E-utiliies) are nine application program interfaces (API) that enable you to gather data from 40 NCBI databases covering a variety of biomedical data, including nucleotide and protein sequences, gene records, three-dimensional molecular structures, and the biomedical literature.   

Figure: The Relationship between the User and NCBI Databases with the list of E-utilites as the Interface

![Figure showing the relationship between the User and NCBI databases with the list of E-utilites as the Interface](eutilies/images/about/figure1.png)

Users can interact with the E-Utility APIs via the following options. Click a link to jump to that page.
  * [Internet Browser](eutilities/browser.md)
  * [Commmand Line](eutitlies/commandline.md)
  * [Programmatically](eutitiles/programmatically.md)

## API Base Path
The NCBI API base path is 
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/{   }.fcgi? 

### List of E-Utilities
Replace the brackets with one of the nine E-utilities listed below. For detailed information about each E-utility, click on the name.
  * [einfo](eutilities/einfo.md)  	Retrieves information and statistics about a single database 
  * [esearch](eutilites/esearch.md)  	Finds text in a single NCBI database
  *	[egquery](eutilities/egquery.md)  	Searches a text query in all Entrez databases and returns the number of results [IN THE FORM OF UID PERHAPS?]   in each database 
  *	[efetch](eutilities/efetch)  	Retrieves full records for each UID   [ DEFINE “FULL RECORD”]
  *	[esummary](eutilities/esummary.md)  	Retrieves document summaries for each UID (unique identifier)
  *	[elink](eutilities/elink.md)  	Retrieves UIDs for related or linked records, or LinkOut URLs  [WHAT IS A LINKOUT URL?]
  *	[espell](eutilities/espell.md)  	Retrieves spelling suggestions for a text query […FOR WHEN YOU DON’T KNOW HOW TO SPELL SOMETHING?]
  *	[ecitmatch](eutilities/ecitmatch.md)  	Searches PubMed for a series of citation strings   [DEFINE CITATION STRING]
  *	[epost](eutilities/epost.md)  	Uploads a list of UIDs for later use [ TO USE LATER HOW?]



## NCBI Databases
There are about 40 NCBI databases. The number changes as databases configurations improve. 
Database names have an abbreviated alias used with API Searches. 
For example:
  *	PM – PubMed database UID prefix
  *	C – PubChem Compound database UID prefix
  *	MMDB -  Molecular Modeling Database 

For the complete list of databases with descriptions see [NCBI Databases](euilities/databases.md).



## Parameter
When you do not know the UIDs of the records you want, include parameters in your search to narrow the results. Add the first parameter with limiting value after the ? of the base path. If you have more than one parameter, add the ampersand (&) then the next parameter with the value. For lists, use a comma between items.

**Example**

base path/esummary.fcgi?db=<database>&id=<uid_list>
base path/esummary.fcgi?db=SRA&ui=646232,932456

### E-utiliy Parameters

The parameters for each E-utiliy are listed on the E-Utility page. See the [List of E-utilities](###-list-of-e-utilties) above and click on the name of the E-utilitiy to go to that E-Utility's page.

There are ## number of E-utility parameters. For complete infomration, see [Paramaters](LINK TO PARAMETERS PAGE).

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
