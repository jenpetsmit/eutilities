# Getting Started with E-utilities

Entrez Utilities (E-Utilities) is an Application Program Interface (API) that helps you gather data from most of the 40 NCBI Entrez database residing at the NCBI using queries. The databases include a variety of biomedical data, including nucleotide and protein sequences, gene records, three-dimensional molecular structures, and the biomedical literature.  The E-Utilities give you control over what fields to search, the data to retrieve, the data format, and how to share results. 

 
**MOVE THIS section**  

Users can interact with the E-Utility APIs via the following options. Click a link to jump to that page. 
  * [Internet Browser](./access/browser.md)
  * [Unix Commmand Line](./access/commandline.md)


## API Query URL

Entrez API queries URL have three parts:
 * Base URL
 * E-Utility
 * Parameters

## Building a Simple Entrez Query URL

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
   

## E-Utilities Parameters
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


## API Key

Without an API key, any site (IP address) posting more than 3 requests per second to the E-Utilities will receive an error message. By including an API key, a site can post up to 10 requests per second by default. Higher rates are available by request (email at email). 

**Example Error Message if Rates are Exceeded**

```{"error":"API rate limit exceeded","count":"11"}```

  
### Obtain an API Key

To get your own API key to use with NCBI E-Utilities, follow these steps:
 1. While signed in to your My NCBI account, go to your [NCBI Account Settings](https://account.ncbi.nlm.nih.gov/settings/). If you don’t have a My NCBI account, you’ll need to create one.
 2. Scroll to the bottom of the page to find the **API Key Management** section.
 3. Click the **Create API Key** button. A unique sequence of characters will be generated and displayed in the “API Key Management” box. This is your API key.
    
Only one API key is allowed per NCBI account. You may request a new key at any time. Requests for new API Keys invalidate any existing API key associated with that NCBI account.

**Use Your API Key with NCBI E-Utilities**   [COPIED FROM DATASETS - CHECK THIS IS TRUE FOR E-UTILITIES]
You can use your API key with the E-Utilites command-line tools and API. To use your API key with the E-Utilties command-line tool EDriect, you have two options:
  * Add your API key as a parameter in each command

To use your API key as a parameter in a command, use the --api-key flag:

```esummary.fcgi?db=pubmed&id=123456&api_key=<PUT_YOUR_API_KEY_HERE>```
  * Alternatively, you can set the NCBI_API_KEY environment variable, and the command-line tool will use the API key automatically. Use export to set the environment variable as follows:

```export NCBI_API_KEY=<PUT_YOUR_API_KEY_HERE>```

**Note**: Curly braces {  } indicate what needs to be replaced. Do not include the curly braces in your API query.

### Usage Guidelines

In order not to overload the E-utility servers, NCBI recommends the following:

  * Users post no more than three URL requests per second.
  * Users limit large jobs to either weekends or between 9:00 PM and 5:00 AM Eastern time during weekdays.

Failure to comply with this policy may result in an IP address being blocked from accessing NCBI. If NCBI blocks an IP address, service will not be restored unless the developers of the software accessing the E-utilities register values of the tool and email parameters with NCBI. 

**Note:** Once tool and email values are registered, all subsequent E-utility requests from that software package should contain both values. 

**Register Your Tool and Email Values**
To register tool and email values, e-mail [eutilities@ncbi.nlm.nih.gov](mailto:eutilities@ncbi.nlm.nih.gov). Include the following information: 
  * The name of either a developer or the organization creating the software
  * The tool values
    ‒	The value of tool should be a string with no internal spaces that uniquely identifies the software producing the request. 
  * The email values 
    ‒	The value of email should be a complete and valid e-mail address of the software developer and not that of a third-party end user. 

The email will be used only to contact developers if NCBI observes requests that violate our policies. We will attempt such contact prior to blocking access. In addition, developers may request that the email be added to the E-Utility mailing list that provides announcements of software updates, known bugs, and other policy changes affecting the E-utilities. 

Once NCBI establishes communication with a developer, receives values for tool and email, and validates the e-mail address in email, the block will be lifted. 

The values for tool and email  must be registered with NCBI. Providing values for tool and email in requests is not sufficient to comply with this policy. Requests from any IP that lack registered values for tool and email and that violate the above usage policies may be blocked. Software developers may register values of tool and email at any time and are encouraged to do so.



