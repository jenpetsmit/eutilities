# EPost

**Base URL**
```
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/epost.fcgi?
```
**Functions**

Creates a search history by:
  * Uploading a list of UIDs to the Entrez History server
  * Appending a list of UIDs to an existing set of UID lists attached to a Web Environment
  * Creating Web environment (&WebEnv) and query key (&query_key) parameters that specify the location of the list of uploaded UIDs on the Entrez history server to use on subsequent queries

## Required Parameters for EPost 

Table 1. Required Parameters for EPost
|  Required Parameter | Common Name | Description |
| --- | --- | --- |
| db  | Database |  Database containing the UIDs in the input list. The value must be a valid Entrez database name (default = pubmed). |
| id | UID | Either a single UID or a comma-delimited list of UIDs may be provided. All of the UIDs must be from the database specified by db. |

 
Notes:
  * For PubMed, no more than 10,000 UIDs can be included in a single URL request.
  * For other databases there is no set maximum for the number of UIDs that can be passed to epost, but if more than about 200 UIDs are to be posted, the request should be made using the HTTP POST method.
  * For sequence databases (nuccore, popset, protein), the UID list may be a mixed list of GI numbers and accession.version identifiers.  **I THINK THIS IS NO LONG TRUE - GOT AN ERROR WHEN TESTED**
  * When using **accession.version** identifiers, there is a conversion step that takes place that causes large lists of identifiers to time out, even when using POST. Therefore, we recommend batching these types of requests in sizes of about 500 UIDs or less to avoid retrieving only a partial amount of records from your original POST input list. <br> **NEED TO LINK TO HOW TO DO THIS**.

## Optional Parameter

Table 2. Optional Parameter for EPost
|  Optional Parameter | Common Name | Description |
| --- | --- | --- |
| WebEnv | Web Environment | This parameter specifies the Web Environment that will receive the UID list sent by post. EPost will create a new **query key** associated with that Web Environment. Usually, this WebEnv value is obtained from the output of a previous ESearch, EPost or ELink call. If no WebEnv parameter is provided, EPost will create a new Web Environment and post the UID list to query_key 1.


## Examples 
Click the links to see the output in a new tab. <br> 

**Example 1**: Upload two PubMed Ids (19393038,30242208) for later processing. <br>[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/epost.fcgi?epost.fcgi?db=pubmed&id=19393038,30242208](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/epost.fcgi?epost.fcgi?db=pubmed&id=19393038,30242208)
  * Result includes:
    * \<QueryKey\>1\</QueryKey\>
    * \<WebEnv\>MCID_677befaa229c857fb4052780\</WebEnv\>
      * Note your WebEnv code will be different from the one in this example.
 
  **Add an additional Id to the Search History (WebEnv)**

Using the following format, add one or more PubMed UIDs and the WebEnv value from the previous search:
```
  epost.fcgi?db=pubmed&id={uid_list2}&WebEnv=$web1
```

Add an additional PubMed Id 29453458 to search history saved to WebEnv=MCID_677befaa229c857fb4052780. <br>[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/epost.fcgi?epost.fcgi?db=pubmed&id=29453458&WebEnv=MCID_677befaa229c857fb4052780](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/epost.fcgi?epost.fcgi?db=pubmed&id=29453458&WebEnv=MCID_677befaa229c857fb4052780)

The WebEnv now contains the results of both posts ($key1 and $key2)

  * Result shows:
    * \<QueryKey\>2\</QueryKey\>
    * \<WebEnv\>MCID_677befaa229c857fb4052780\</WebEnv\>
 

** DELETE AFTER CONFIRMING "UID list may be a mixed list of GI numbers and accession.version identifiers" works or not**
  
  
      * **Example 2**: Upload Protein UIDs for later processing. <br> [https://eutils.ncbi.nlm.nih.gov/entrez/eutils/epost.fcgi?epost.fcgi?db=protein&id=15718680,NP_001098858.1,119703751](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/epost.fcgi?epost.fcgi?db=protein&id=15718680,NP_001098858.1,119703751)
    
    
                   
     
    
    
    
    
