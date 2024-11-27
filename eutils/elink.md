# ELink

Records in one database are often linked to records in a different database showing the two sets of records are related. For example a record in the SRA database is linked to a record in the BioProject database. If you have data from one database (use the dbfrom parameter), you can see what records in a second database (use the db parameter) may be linked.

ELink retrieves UIDs for records linked to your list of UIDs. ELink also  retrieves LinkOut URLs, which are links to journals in PubMed database.

**Base URL**

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi```

**Functions**

  * Retrieve UIDs linked to an input set of UIDs in either the same or a different Entrez database
  * Retrieve UIDs linked to other UIDs in the same Entrez database that match an Entrez query
  * Checks for the existence of Entrez links for a set of UIDs within the same database
  * Lists the available links for a UID
  * Lists LinkOut URLs and attributes for a set of UIDs
  * Lists hyperlinks to primary LinkOut providers for a set of UIDs
  * Creates hyperlinks to the primary LinkOut provider for a single UID

## Required Parameters

**Table 1. ELink Required Parameters**
 |  Required Parameters | Common Name | Brief Description |
 | --- | --- | --- |
 | db  | Target database  |  Database from which to retrieve UIDs |
 | dbfrom  | Source database  | Database containing the input UIDs |
 | cmd | Command option | Command parameter which enables additional filtering |
 |  cmd=neighbor_score |    Neighbor score       |   Retrieves  a set of UIDs within the same database as the input UIDs along with computed similarity scores     | 
  |  cmd=neighbor_history  | Neighbor history   |     Output UIDs are saved (posted) to the Entrez History server for use in subsequent call   | 
   |  cmd=acheck |   Checks for available links         |    Retrieves links available for a set of UIDs   | 
    |  cmd=ncheck |   Checks for links in same database         |      Retrieves links in same database   | 
     |  cmd=lcheck|   External links (LinkOuts)         | Retreives external links (PubMed)       | 
      |  cmd=llinks |    External links that are not libraries        |    For each input UID, ELink lists the URLs and attributes for the LinkOut providers that are not libraries .   | 
       |  cmd=llinkslib | External links that include libraries    |   For each input UID, ELink lists the URLs and attributes for all LinkOut providers including libraries    | 
        |  cmd=prlinks |      Primary LinkOut provider      | For each input UID retrieves the primary LinkOut provider, or links directly to the LinkOut provider's web site for a single UID if retmode is set to ref.      | 
 

 

###	 Batch Mode – Finds Only One Set of Linked UIDs

```elink.fcgi?dbfrom={source_db}&db={destination_db}&id={uid_list}```

**Input**: List of UIDs (&id); Source Entrez database (&dbfrom); Destination Entrez database (&db) 

**Output**: XML containing linked UIDs from source and destination databases   

**Example**: Find one set of Gene IDs (DESTINATION DB) linked to nuccore (SOURCE DB) GIs 34577062 and 24475906

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=nuccore&db=gene&id=34577062,24475906](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=nuccore&db=gene&id=34577062,24475906)
 

###	‘By Id’ mode – finds one set of linked UIDs for each input UID

```elink.fcgi?dbfrom={source_db}&db={destination_db}&id={uid1}&id={uid2}&id={uid3}...```

**Example**: Find separate sets of Gene IDs linked to nuccore GIs 34577062 and 24475906

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=nuccore&db=gene&id=34577062&id=24475906](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=nuccore&db=gene&id=34577062&id=24475906)

**Note**: The parameter, &db, may be a comma-delimited list of databases, so that elink returns multiple sets of linked UIDs in a single call.
_____________________________________________________
 

### Finding Links to Data from a Previous Search

1. First search using the esearch E-Utility, which create Web Environment value ($web1) and Query Key ($key1) value.  
```esearch.fcgi?db={source_db}&term={query}&usehistory=y```

2. Next use the WebEnv and query_key values in a subsequent elink call. 

```elink.fcgi?dbfrom={source_db}&db={destination_db}&query_key=$key1&WebEnv=$web1&cmd=neighbor_history```

**Input**: 
  * Source Entrez database (&dbfrom)
  * Destination Entrez database (&db)
  * Web environment (&WebEnv)
  * query key (&query_key) representing the set of source UIDs on the Entrez history server
  * Command mode (&cmd)

**Output**: XML containing Web environments and query keys for each set of linked UIDs

**Note**: To achieve ‘By Id’ mode, you must enter each input UID as a separate &id parameter in the URL. If not, sending a WebEnv/query_key set produces Batch mode behavior retrieving one set of linked UIDs.



## ELink Command Options

ELink offers the option to write commands in the API elink query.

**Computational Neighbors**

If db and dbfrom are set to the same database value, then ELink will return computational neighbors within that database. Please see the full list of Entrez links for available computational neighbors. Computational neighbors have linknames that begin with dbname_dbname (examples: protein_protein, pcassay_pcassay_activityneighbor).

### cmd=neighbor (default)

ELink returns a set of UIDs in db linked to the input UIDs in dbfrom.

**Example**: Link from protein to gene

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=gene&id=15718680,157427902](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=gene&id=15718680,157427902)

## Computational Neighbors
ELink can return a set of UIDs within the same database as the input UIDs along with computed similarity scores called _Computational Neighbors_.

### cmd=neighbor_score

**Example**: Find related articles to PMID 20210808

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&db=pubmed&id=20210808&cmd=neighbor_score](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&db=pubmed&id=20210808&cmd=neighbor_score)

### cmd=neighbor_history

```elink.fcgi?dbfrom={source_db}&db={source_db}&id={uid_list}&term={query}&cmd=neighbor_history```

ELink posts the output UIDs to the Entrez History server and returns a query_key and WebEnv corresponding to the location of the output set.

**Example**: Link from protein to gene and post the results on the Entrez History

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=gene&id=15718680,157427902&cmd=neighbor_history](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=gene&id=15718680,157427902&cmd=neighbor_history)

### 	Finding Computational Neighbors Limited by an Entrez Search

**Input**: Source Entrez database (&dbfrom); Destination Entrez database (&db); List of UIDs (&id); Entrez query (&term); Command mode (&cmd)

**Output**: XML containing Web environments and query keys for each set of linked UIDs

**Example**: Find protein UIDs that are rat Reference Sequences and that are sequence similar to GI 15718680

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=protein&id=15718680&term=rat[orgn]+AND+srcdb+refseq[prop]&cmd=neighbor_history](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=protein&id=15718680&term=rat[orgn]+AND+srcdb+refseq[prop]&cmd=neighbor_history)





### cmd=acheck
ELink lists all links available for a set of UIDs.

**Example**: List all possible links from two protein GIs

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&id=15718680,157427902&cmd=acheck](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&id=15718680,157427902&cmd=acheck)

**Example**: List all possible links from two protein GIs to PubMed

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=pubmed&id=15718680,157427902&cmd=acheck](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=pubmed&id=15718680,157427902&cmd=acheck)

### cmd=ncheck
ELink checks for the existence of links within the same database for a set of UIDs. These links are equivalent to setting db and dbfrom to the same value.

**Example**: Check whether two nuccore sequences have "related sequences" links.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=nuccore&id=21614549,219152114&cmd=ncheck](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=nuccore&id=21614549,219152114&cmd=ncheck)

### cmd=lcheck
Elink checks for the existence of external links (LinkOuts) for a set of UIDs.

**Example**: Check whether two protein sequences have any LinkOut providers.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&id=15718680,157427902&cmd=lcheck](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&id=15718680,157427902&cmd=lcheck)

### cmd=llinks
For each input UID, ELink lists the URLs and attributes for the LinkOut providers that are not libraries.

**Example**: List the LinkOut URLs for non-library providers for two pubmed abstracts.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848,19822630&cmd=llinks](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848,19822630&cmd=llinks)
### cmd=llinkslib
For each input UID, ELink lists the URLs and attributes for all LinkOut providers including libraries.

**Example**: List all LinkOut URLs for two PubMed abstracts.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848,19822630&cmd=llinkslib](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848,19822630&cmd=llinkslib)

### cmd=prlinks
ELink lists the primary LinkOut provider for each input UID, or links directly to the LinkOut provider's web site for a single UID if retmode is set to ref.

**Example**: Find links to full text providers for two PubMed abstracts.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848,19822630&cmd=prlinks](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848,19822630&cmd=prlinks)

**Example**: Link directly to the full text for a PubMed abstract at the provider's web site.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848&cmd=prlinks&retmode=ref](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848&cmd=prlinks&retmode=ref)





