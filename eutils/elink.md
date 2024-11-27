# ELink

**Base URL**

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi```

 Retrieves UIDs for related or linked records, or LinkOut URLs.

Functions
 •	Returns UIDs linked to an input set of UIDs in either the same or a different Entrez database
 •	Returns UIDs linked to other UIDs in the same Entrez database that match an Entrez query
 •	Checks for the existence of Entrez links for a set of UIDs within the same database
 •	Lists the available links for a UID
 •	Lists LinkOut URLs and attributes for a set of UIDs
 •	Lists hyperlinks to primary LinkOut providers for a set of UIDs
 •	Creates hyperlinks to the primary LinkOut provider for a single UID
K-1	Required Parameters
db
Database from which to retrieve UIDs. The value must be a valid Entrez database name (default = pubmed). This is the destination database for the link operation.
dbfrom
Database containing the input UIDs. The value must be a valid Entrez database name (default = pubmed). This is the origin database of the link operation. If db and dbfrom are set to the same database value, then ELink will return computational neighbors within that database. Please see the full list of Entrez links for available computational neighbors. Computational neighbors have linknames that begin with dbname_dbname (examples: protein_protein, pcassay_pcassay_activityneighbor).

K-2	 Batch mode – finds only one set of linked UIDs
elink.fcgi?dbfrom={source_db}&db={destination_db}&id={uid_list}

Input: List of UIDs (&id); Source Entrez database (&dbfrom); Destination Entrez database (&db)
Output: XML containing linked UIDs from source and destination databases  [ I think this means, UIDS that are in both source and destination databases ]
Example: Find one set of Gene IDs (DESTINATION DB) linked to nuccore (SOURCE DB) GIs 34577062 and 24475906
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=nuccore&db=gene&id=34577062,24475906
 
K-3	‘By Id’ mode – finds one set of linked UIDs for each input UID
elink.fcgi?dbfrom={source_db}&db={destination_db}&id={uid1}&id={uid2}&id={uid3}...
Example: Find separate sets of Gene IDs linked to nuccore GIs 34577062 and 24475906
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=nuccore&db=gene&id=34577062&id=24475906
Note: &db may be a comma-delimited list of databases, so that elink returns multiple sets of linked UIDs in a single call
_____________________________________________________
 

K-4	Finding Links to Data from a Previous Search
esearch.fcgi?db={source_db}&term={query}&usehistory=y

# esearch produces WebEnv value ($web1) and QueryKey value ($key1)

elink.fcgi?dbfrom={source_db}&db={destination_db}&query_key=$key1&WebEnv=$web1&cmd=neighbor_history
Input: Source Entrez database (&dbfrom); Destination Entrez database (&db); Web environment (&WebEnv) and query key (&query_key) representing the set of source UIDs on the Entrez history server; Command mode (&cmd)
Output: XML containing Web environments and query keys for each set of linked UIDs
Note: To achieve ‘By Id’ mode, one must send each input UID as a separate &id parameter in the URL. Sending a WebEnv/query_key set always produces Batch mode behavior (one set of linked UIDs).
K-5	Finding Computational Neighbors Limited by an Entrez Search
elink.fcgi?dbfrom={source_db}&db={source_db}&id={uid_list}&term={query}&cmd=neighbor_history
Input: Source Entrez database (&dbfrom); Destination Entrez database (&db); List of UIDs (&id); Entrez query (&term); Command mode (&cmd)
Output: XML containing Web environments and query keys for each set of linked UIDs
Example: Find protein UIDs that are rat Reference Sequences and that are sequence similar to GI 15718680
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=protein&id=15718680&term=rat[orgn]+AND+srcdb+refseq[prop]&cmd=neighbor_history

