# API Key
   
Since December 1, 2018, NCBI has provided API keys that offer enhanced levels of supported access to the E-utilities. Without an API key, any site (IP address) posting more than 3 requests per second to the E-utilities will receive an error message. By including an API key, a site can post up to 10 requests per second by default. Higher rates are available by request (vog.hin.mln.ibcn@seitilitue). 

EDirect programs are designed to work on large sets of data. Although not required, for best performance, include an NCBI API Key. To use, place the following line in your .bash_profile and .zshrc configuration files:  **<--How to do this? WHERE IS CONFIGURATION FILE? -->**

  `export NCBI_API_KEY=your_NCBI_api_key`

## Get your API key
To get your API key, follow these steps:
1. While signed in to your My NCBI account, go to your [NCBI Account Settings](https://account.ncbi.nlm.nih.gov/settings/). If you don’t have a My NCBI account, you’ll need to create one.
2. Scroll to the bottom of the page to find the _API Key Management_ section.
3. Click the **Create API Key**  button. A unique sequence of characters will be generated and displayed in the  _API Key Management_  box. This is your API key.

Only one API key is allowed per NCBI account. You may request a new key at any time. Any existing API keys associated with that NCBI account will become invalid.


### Errors and Limits 
**Example error message if rates are exceeded**

`{"error":"API rate limit exceeded","count":"11"}`

#### Minimizing the Number of Requests   **FIX OR MOVE THIS LATER**
If a task requires searching for and/or downloading a large number of records,  use the Entrez History to upload and retrieve these records in batches rather than using separate requests for each record. 
Please refer to Application 3 in Chapter 3 for an example. Many thousands of IDs can be uploaded using a single EPost request, and several hundred records can be downloaded using one EFetch request.

