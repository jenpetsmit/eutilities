# E-Utilities

Note: This website is a work in progress.

Entrez Utilities (E-Utilities) is an Application Program Interface (API) that helps you gather data from most of the 40 NCBI Entrez databases (with greater than 1 billion records) residing at the NCBI using queries. The databases include a variety of biomedical data, including biomedical literature nucleotide and protein sequences, gene records, gene expression, genotype and biological assay studies with data, chemical information, and three-dimensional molecular structures. There are about 25 million EUtilities calls sent to our servers daily from about 100,000 different IP addresses.



Here are a few examples of what E-Utilites can do for you:
   * Search PubMed with a term and retrive PMIDs **(Add link here to ID)**
   * Search MedGen with a SnoMedCI ID, then link over to GTR and retrieve their Summary info
   * Save a list of Gene IDs and fetch their full records
   * Save a PubChem Compound CID and retrieve the SDF-formatted record to showthe 3D coordinates in the Molecules App **(ADD LINK HERE)**

You can access E-utilities by writing URLs and pasting them into any internet browser. To see what information is available, review the [available databases and the data](https://www.ncbi.nlm.nih.gov/search/) they each offer. 


## API Query URL

Entrez API queries URL have three parts:
 * Base URL
 * E-Utility
 * Parameters



Figure 1. Parts of the Entrez API Query

 ![Parts of the Entrez API Query](apiurlparts.png) 
## Building a Simple Entrez Query URL
You can build a simple API query URL in your internet browser: 

 1. Start your Entrez query with the following base URL:
    
```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/```

 2.	Add an **E-Utility** plus “.fcgi?”
    
```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/E-Utility.fcgi?```

   *	See [Table 1](#table1) below for a list of E-Utilities with descriptions.

 3.	Add required and optional parameters

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/E_Utilitiy.fcgi?parameters```

   *	See Table 2 for a list of parameters with descriptions
 
Here is an example of a simple API Entrez query. You can click the link or copy and paste the Entrez API URL in an internet browser to see how browser-based access works:

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?db=pubmed&id=19393038](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?db=pubmed&id=19393038)
  

### E-Utilities
The Entrez API includes nine E-Utilities. In Table 1, see the list of E-Utilities with a short description.  
Each E-Utility name is linked to its own page with complete information.  

**<a id="table1"></a>Table 1.  List of Entrez API E-Utilities**

| E-Utility   | Brief Description | 
| --- | --- |
| [EInfo](einfo.md)   |  Retrieves information and statistics about a single database <br>  If no database is provide, einfo returns the list of current databases in the Entrez network. |
| [ESearch](esearch.md)    | Returns a list of UIDs from a single database containing the searched text    |
| [ESummary](esummary.md)  	  |  Downloads document summaries for each UID   |
| [EFetch](efetch.md) | Returns a full data record   |
| [ELink](elink.md)     |  Retrieves UIDs for related or linked records, or LinkOut URLs     |
| [EGQuery](egquery.md)     |  Searches a text query in all Entrez databases and returns the number of results [IN THE FORM OF UID PERHAPS?]   in each database   |
| [ESpell](espell.md)     |  	Retrieves spelling suggestions for a text query   |
| [ECitmatch](ecitmatch.md)  	  |  Searches PubMed for a series of citation strings    |
|	[EPost](epost.md)   |  Saves a list of UIDs you can use subsequently with other E-Utilities like esummary or efetch   |
   

## E-Utilities Parameters
Parameters are options you add to the base URL and E-Utility to limit the results.  Each E-Utility has required and optional parameters. Null values or inappropriate parameters are generally ignored
See Table 2 for a list of the most often used parameters.  

 * For a full list, see [E-Utilities Parameters](parameters.md) page to see the required and optional parameter options for each E-Utility.

**Table 2: Most Often Used Parameters [THIS PROBABALY NEEDS MORE WORK]**

| Common name      | Works&nbsp;with          | What does it do?         | Entrez API abbriviation  **what to call this?**             | Example     |
| --- | ---  | ---  | ---  | ---  |
| Database | EInfo<br> ESearch<br> ESummary<br> EPost<br> ELink<br> ESpell<br> ECitmatch<br>EFetch  | Limits results to the provided database | db={entrez database query name}   | db=gap  |  
| Term    | EGQuery<br> ESearch<br> ELink<br> ESpell        | Includes the term you provide in the query     | term={text}     | term=asthma     |
| UID list      | ESummary<br>EPost<br> ELink<br> EFetch       | Limits results to the provided UIDs    | id={UID}     | id=19393038,30242208,29453458      |
| Use History      | ESearch      | Use history flag            | usehistory=y       |    usehistory=y                   |
| Return max      | ESearch<br>esummary         | Total number of DocSums from the input set to be retrieved, up to a maximum of 10,000 | retmax={maximum number of results you want}      | retmax=10       |
| Retrieval mode   | ESummary<br> EInfo<br> ESearch<br> EFetch<br> ELink     | Formats of the output       | retmode={format}      | retmode=json<br> retmode=xml<br> XML is the default<BR> All E-Utilities support JSON except efetch  |
| Relative Date       | ESearch       | Sets the days to be searched relative to the current date   | reldate=        | reldate=5 IS THIS EXAMPLE RIGHT? IS this plus or minus today's date?     |
| Minimum Date   | ESearch<br> ELink       | Specifies the start date according to the format YYYY/MM/DD<br> YYYY<br> or YYYY/MM | mindate={YYYY/MM/DD} <br> mindate={YYYY/MM} <br> mindate={YYYY}    | mindate=2022/12 <br>A query must contain both mindate and maxdate parameters    |
| Maximum Date | ESearch<br> ELink       | Specifies the end date according to the format YYYY/MM/DD<br> YYYY<br> or YYYY/MM |  maxdate={YYYY/MM/DD} <br> maxdate={YYYY/MM} <br> maxdate={YYYY}     | maxdate=2024/12 <br> A query must contain both mindate and maxdate parameters    |
| Retrieval Type     | ECitmatch<br> EFetch<br> EInfo<br> ELink<br> ESummary<br> ESearch  | retype={ WHAT GOES HERE?}  | retype= EXAMPLE <br> Return types vary by E=Utility  |


 



## 	Rules of Writing Entrez API URLs
This section provides guidance to writing Entrez API URLs regarding ASCII limits, spaces, and case.  For very long queries (more than several hundred characters long), consider using an HTTP POST call. 

**ASCII Rules**

URLs can only be sent over the Internet using the ASCII character-set. Some Entrez URLs contain characters outside the ASCII set, so those characters have to be encoded into a valid ASCII format.
For example, quotation marks (“) and the octothorpe (#) symbol  are not ASCII characters. See Table 3 for a list of non-ASCII characters commonly used in Entrez URLs and their encoded substitutions.

**Table 3: Non-ASCII characters commonly used in Entrez URLs and their encoded substitutions**
|  Non ASCII Characters | Common Names | Encoded Substitutions | Example |
| --- | --- | --- | --- | 
| " | Quotation Marks | %22 |  ENTER EXAMPLE HERE |
| # | Octothorpe/ Hashtag/Pound Sign | %23 |ENTER EXAMPLE HERE |
| OTHER ? | --- | --- | ENTER EXAMPLE HERE |

### ASCII Encoding Examples

Search term = #2 and “gene in genomic”                              <-  CAN WE CHANGE THE 2 TO 5?

Incorrect:  &term=#2+AND+"gene in genomic"[properties]               <-- THE BRACKETS ARE WAY CONFUSING

Correct:   &term=%232+AND+%22gene+in+genomic%22[properties]

### Use of Spaces

Do not include spaces in the URLs, particularly in queries. If a space is required, use a plus sign (+) instead of a space:

Incorrect:  &id=352, 25125, 234
 
 Correct:   &id=352,25125,234

Incorrect:  &term=biomol mrna[properties] AND mouse[organism]

Correct:   &term=biomol+mrna[properties]+AND+mouse[organism]

### Use of Lower- and Upper-Case

When constructing URLs for the E-utilities, use lowercase characters for all parameters except for the **WebEnv** parameter. 

## Reponse
An XML formatted reponse returns.

Returns have a default limit of a maximum of 20. To change the default limit see _retmax_ on the [Parameter's Page](eutilities/parameters.md#retmax)
  
