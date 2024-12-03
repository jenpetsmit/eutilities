# API Key
   
NCBI provides each user an API key, which provides an enhanced level of supported access to the E-utilities. Without an API key, any site (IP address) posting more than 3 requests per second to the E-utilities will receive an error message. By including an API key, a site can post up to 10 requests per second by default. Higher rates are available by request at [eutilities@ncbi.nlm.nih.gov](mailto:eutilities@ncbi.nlm.nih.gov). 

**Example Error Message if Rates are Exceeded**

```{"error":"API rate limit exceeded","count":"11"}```

EDirect programs are designed to work on large sets of data. Although not required, for best performance, include an NCBI API Key. To use, place the following line in your .bash_profile and .zshrc configuration files:  **<--How to do this? WHERE IS CONFIGURATION FILE? -->**

  `export NCBI_API_KEY=your_NCBI_api_key`

## Get your API key
To get your API key, follow these steps:
1. While signed in to your My NCBI account, go to your [NCBI Account Settings](https://account.ncbi.nlm.nih.gov/settings/). If you don’t have a My NCBI account, you’ll need to create one.
2. Scroll to the bottom of the page to find the _API Key Management_ section.
3. Click the **Create API Key**  button. A unique sequence of characters will be generated and displayed in the  _API Key Management_  box. This is your API key.

Only one API key is allowed per NCBI account. You may request a new key at any time. Any existing API keys associated with that NCBI account will become invalid.



#### Minimizing the Number of Requests   **FIX OR MOVE THIS LATER**
If a task requires searching for and/or downloading a large number of records,  use the Entrez History to upload and retrieve these records in batches rather than using separate requests for each record. 
Please refer to Application 3 in Chapter 3 for an example. Many thousands of IDs can be uploaded using a single EPost request, and several hundred records can be downloaded using one EFetch request.

  

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
