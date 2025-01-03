# EPost

**Base URL**
```
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/epost.fcgi
```
**Functions**
  * Uploads a list of UIDs to the Entrez History server
  * Appends a list of UIDs to an existing set of UID lists attached to a Web Environment

**Required Parameters**

db
  * Database containing the UIDs in the input list. The value must be a valid Entrez database name (default = pubmed).
id
  * UID list. Either a single UID or a comma-delimited list of UIDs may be provided.
  * All of the UIDs must be from the database specified by db.
  * For PubMed, no more than 10,000 UIDs can be included in a single URL request.
  * For other databases there is no set maximum for the number of UIDs that can be passed to epost, but if more than about 200 UIDs are to be posted, the request should be made using the HTTP POST method.
  * For sequence databases (nuccore, popset, protein), the UID list may be a mixed list of GI numbers and accession.version identifiers.

Note: When using accession.version identifiers, there is a conversion step that takes place that causes large lists of identifiers to time out, even when using POST. Therefore, we recommend batching these types of requests in sizes of about 500 UIDs or less to avoid retrieving only a partial amount of records from your original POST input list.

epost.fcgi?db=pubmed&id=19393038,30242208,29453458
epost.fcgi?db=protein&id=15718680,NP_001098858.1,119703751

**Optional Parameter**

**WebEnv**
  * Web Environment. If provided, this parameter specifies the Web Environment that will receive the UID list sent by post. EPost will create a new query key associated with that Web Environment. Usually, this WebEnv value is obtained from the output of a previous ESearch, EPost or ELink call. If no WebEnv parameter is provided, EPost will create a new Web Environment and post the UID list to query_key 1.
epost.fcgi?db=protein&id=15718680,157427902,119703751&WebEnv={webenv string}
  * Example: Post records to PubMed:<br>
[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/epost.fcgi?db=pubmed&id=11237011,12466850](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/epost.fcgi?db=pubmed&id=11237011,12466850)


**Basic Uploading (Creating a Search History)**

epost.fcgi?db={database}&id={uid_list}

  * **Input**: List of UIDs (&id); Entrez database (&db)
  * **Output**: Web environment (&WebEnv) and query key (&query_key) parameters specifying the location on the Entrez history server of the list of uploaded UIDs
  * **Example**: Upload five Gene IDs (7173,22018,54314,403521,525013) for later processing.<br>[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/epost.fcgi?db=gene&id=7173,22018,54314,403521,525013[(****)

** Associating a Set of UIDs with Previously Posted Sets**
```
epost.fcgi?db={database1}&id={uid_list1}
```
# epost produces WebEnv value ($web1) and QueryKey value ($key1)
```
epost.fcgi?db={database2}&id={uid_list2}&WebEnv=$web1
```
# epost produces WebEnv value ($web2) that contains the results of both 
posts ($key1 and $key2)

  * **Input**: List of UIDs (&id); Entrez database (&db); Existing web environment (&WebEnv)
  * **Output**: Web environment (&WebEnv) and query key (&query_key) parameters specifying the location on the Entrez history server of the list of uploaded UIDs
