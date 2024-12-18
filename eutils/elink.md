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
 | db=<database>  | Target database  |  Database from which to retrieve UIDs |
 | dbfrom=<source database>  | Source database  | Database containing the input UIDs |
 |  cmd=neighbor_score |    Neighbor score       |   Retrieves  a set of UIDs within the same database as the input UIDs along with computed similarity scores     | 
 |  cmd=neighbor_history  | Neighbor history   |     Output UIDs are saved (posted) to the Entrez History server for use in subsequent call   | 
 |  cmd=acheck |   Checks for available links         |    Retrieves links available for a set of UIDs   | 
 |  cmd=ncheck |   Checks for links in same database         |      Retrieves links in same database   | 
 |  cmd=lcheck|   External links (LinkOuts)         | Retreives external links (PubMed)       | 
 |  cmd=llinks |    External links that are not libraries        |    For each input UID, ELink lists the URLs and attributes for the LinkOut providers that are not libraries .   | 
 |  cmd=llinkslib | External links that include libraries    |   For each input UID, ELink lists the URLs and attributes for all LinkOut providers including libraries    | 
 |  cmd=prlinks |      Primary LinkOut provider      | For each input UID retrieves the primary LinkOut provider, or links directly to the LinkOut provider's web site for a single UID if retmode is set to ref.      | 
 



## ELink Command Options

ELink offers the option to write commands in the API ELink query.

**Computational Neighbors**

If db and dbfrom are set to the same database value, then ELink will return computational neighbors within that database. Please see the full list of Entrez links for available computational neighbors. Computational neighbors have linknames that begin with dbname_dbname (examples: protein_protein, pcassay_pcassay_activityneighbor).
<br>

|   Command parameter | Description |
| --- | --- |
| cmd=neighbor | ELink returns a set of UIDs in db linked to the input UIDs in dbfrom. |

 **Example**: Link from protein to gene

 [https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=gene&id=15718680,157427902](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=gene&id=15718680,157427902)
<br>

**Computational Neighbors**
ELink can return a set of UIDs within the same database as the input UIDs along with computed similarity scores called _Computational Neighbors_.

<br>

|   Command parameter | Description |
| --- | --- |
|cmd=neighbor_score |  Computed similarity scores  |

**Example**: Find related articles to PMID 20210808

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&db=pubmed&id=20210808&cmd=neighbor_score](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&db=pubmed&id=20210808&cmd=neighbor_score)
<br>


|   Command parameter | Description |
| --- | --- |
| cmd=neighbor_history** |      NEED DESCRIPTION |

```elink.fcgi?dbfrom={source_db}&db={source_db}&id={uid_list}&term={query}&cmd=neighbor_history```

ELink posts the output UIDs to the Entrez History server and returns a query_key and WebEnv corresponding to the location of the output set.

**Example**: Link from protein to gene and post the results on the Entrez History

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=gene&id=15718680,157427902&cmd=neighbor_history](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=gene&id=15718680,157427902&cmd=neighbor_history)
<br>
### 	Finding Computational Neighbors Limited by an Entrez Search

**Input**: Source Entrez database (&dbfrom); Destination Entrez database (&db); List of UIDs (&id); Entrez query (&term); Command mode (&cmd)

**Output**: XML containing Web environments and query keys for each set of linked UIDs

**Example**: Find protein UIDs that are rat Reference Sequences and that are sequence similar to GI 15718680

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=protein&id=15718680&term=rat[orgn]+AND+srcdb+refseq[prop]&cmd=neighbor_history](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=protein&id=15718680&term=rat[orgn]+AND+srcdb+refseq[prop]&cmd=neighbor_history)




<br>

|   Command parameter | Description |
| --- | --- |
| cmd=acheck | ELink lists all links available for a set of UIDs|

**Example**: List all possible links from two protein GIs

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&id=15718680,157427902&cmd=acheck](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&id=15718680,157427902&cmd=acheck)

**Example**: List all possible links from two protein GIs to PubMed

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=pubmed&id=15718680,157427902&cmd=acheck](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=pubmed&id=15718680,157427902&cmd=acheck)

<br>

|   Command parameter | Description |
| --- | --- |
|cmd=ncheck  | ELink checks for the existence of links within the same database for a set of UIDs. These links are equivalent to setting db and dbfrom to the same value|

**Example**: Check whether two nuccore sequences have "related sequences" links.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=nuccore&id=21614549,219152114&cmd=ncheck](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=nuccore&id=21614549,219152114&cmd=ncheck)
<br>
**cmd=lcheck**
Elink checks for the existence of external links (LinkOuts) for a set of UIDs.

**Example**: Check whether two protein sequences have any LinkOut providers.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&id=15718680,157427902&cmd=lcheck](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&id=15718680,157427902&cmd=lcheck)
<br>

**cmd=llinks**
For each input UID, ELink lists the URLs and attributes for the LinkOut providers that are not libraries.

**Example**: List the LinkOut URLs for non-library providers for two pubmed abstracts.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848,19822630&cmd=llinks](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848,19822630&cmd=llinks)
<br>

**cmd=llinkslib**
For each input UID, ELink lists the URLs and attributes for all LinkOut providers including libraries.

**Example**: List all LinkOut URLs for two PubMed abstracts.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848,19822630&cmd=llinkslib](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848,19822630&cmd=llinkslib)
<br>

**cmd=prlinks**
ELink lists the primary LinkOut provider for each input UID, or links directly to the LinkOut provider's web site for a single UID if retmode is set to ref.

**Example**: Find links to full text providers for two PubMed abstracts.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848,19822630&cmd=prlinks](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848,19822630&cmd=prlinks)

**Example**: Link directly to the full text for a PubMed abstract at the provider's web site.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848&cmd=prlinks&retmode=ref](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&id=19880848&cmd=prlinks&retmode=ref)
<br>
## Optional Parameters

**Table 2. ELink Optional Parameters**
 |  Optional Parameters | Common Name | Brief Description |
 | --- | --- | --- |
 | id | Unique Identifier/UID | Identifies a record in an Entrez Database |
 | query_key | Query Key | This integer represents a UID lists attached to a Web Environment to be used as input to ELink |
 | WebEnv | Web Environment | Represents a saved session from a previous esearch, epost, or elink call |
 | retmode | Retrieval mode | Determines the format of the returned output |
 | idtype | Id Type | The type of identifier to return for sequence databases   |
 | linkname | Name of the Entrez link  | Every link in Entrez is given a name of the form dbfrom_db_subset. |
 | term | Key word or phrase | Text query used to limit the output set of linked UIDs |
 | holding |   | Name of LinkOut provider |
 | datetype | Type of date | One of 3 date types used to limit a link operation |
 | reldate | Relative date | Retrieves only those items that have a date specified by datetype within the last n days. |
 | mindate | Minimum date | Limits a link operation by the earliest date specified by datetype |
 | maxdate | Maximum date | Limits a link operation by the morst recent date specified by datetype |
<br>

**id=<UID>**

  * Either a single UID or a comma-delimited list of UIDs may be provided. 
  * All the UIDs must be from the database specified by dbfrom. 
  * There is no set maximum for the number of UIDs that can be passed to ELink, but if more than about 200 UIDs are to be provided, the request should be made using the HTTP POST method.

**Example**: Link from protein to gene

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=gene&id=15718680,157427902,119703751](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=gene&id=15718680,157427902,119703751)

**Example**: Find related sequences (link from nuccore to nuccore).

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=nuccore&db=nuccore&id=34577062](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=nuccore&db=nuccore&id=34577062)

If more than one id parameter is provided, ELink will perform a separate link operation for the set of UIDs specified by each id parameter. This effectively accomplishes "one-to-one" links and preserves the connection between the input and output UIDs.

**Example**: Find one-to-one links from protein to gene.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=gene&id=15718680&id=157427902&id=119703751](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=gene&id=15718680&id=157427902&id=119703751)

For sequence databases (nuccore, popset, protein), the UID list may be a mixed list of GI numbers and accession.version identifiers.

**Example**: Find one-to-one links from protein to gene.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=gene&id=15718680&id=NP_001098858.1&id=119703751](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=protein&db=gene&id=15718680&id=NP_001098858.1&id=119703751)

K-7	Required Parameters when  input is from the Entrez History server

**query_key**

Query key. This integer specifies which of the UID lists attached to the given Web Environment will be used as input to ELink. Query keys are obtained from the output of previous ESearch, EPost or ELInk calls. The query_key parameter must be used in conjunction with WebEnv.
<br>
**WebEnv**

Web Environment. This parameter specifies the Web Environment that contains the UID list to be provided as input to ELink. Usually, this WebEnv value is obtained from the output of a previous ESearch, EPost or ELink call. The WebEnv parameter must be used in conjunction with query_key.

Link from protein to gene:

```elink.fcgi?dbfrom=protein&db=gene&query_key={key}&WebEnv={webenv string}```

**Example**: Find related sequences (link from protein to protein): elink.fcgi?dbfrom=protein&db=protein&query_key={key}&WebEnv={webenv string}

K-8	Optional Parameter – Retrieval
<br>
**retmode**

Retrieval type. Determines the format of the returned output. The default value is ‘xml’ for ELink XML, but ‘json’ is also supported to return output in JSON format.
<br>
**idtype**

Specifies the type of identifier to return for sequence databases (nuccore, popset, protein). By default, ELink returns GI numbers in its output. If idtype is set to ‘acc’, ELink will return accession.version identifiers rather than GI numbers.
<br>
### Optional Parameters – Limiting the Output Set of Links

**linkname**

Name of the Entrez link to retrieve. Every link in Entrez is given a name of the form dbfrom_db_subset.

The values of subset vary depending on the values of dbfrom and db. Many dbfrom/db combinations have no subset values. See the list of Entrez links for a listing of all available linknames. When linkname is used, only the links with that name will be retrieved.

The linkname parameter only functions when cmd is set to neighbor or neighbor_history.

**Example**: Find all links from gene to snp.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=gene&db=snp&id=93986](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=gene&db=snp&id=93986)

**Example**: Find snps with genotype data linked to genes.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=gene&db=snp&id=93986&linkname=gene_snp_genegenotype](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=gene&db=snp&id=93986&linkname=gene_snp_genegenotype)
<br>
**term**

Entrez query used to limit the output set of linked UIDs. The query in the term parameter will be applied after the link operation, and only those UIDs matching the query will be returned by ELink. The term parameter only functions when db and dbfrom are set to the same database value.

**Example**: Find all related articles for a PMID.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&db=pubmed&id=19879512](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&db=pubmed&id=19879512)

**Example**: Find all related review articles published in 2008 for a PMID.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&db=pubmed&id=19879512&term=review%5Bfilter%5D+AND+2008%5Bpdat%5Dh](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&db=pubmed&id=19879512&term=review%5Bfilter%5D+AND+2008%5Bpdat%5Dh)

<br>
**holding**

Name of LinkOut provider. Only URLs for the LinkOut provider specified by holding will be returned. The value provided to holding should be the abbreviation of the LinkOut provider's name found in the {NameAbbr}tag of the ELink XML output when cmd is set to llinks or llinkslib. The holding parameter only functions when cmd is set to llinks or llinkslib.

**Example**: Find information for all LinkOut providers for a PMID.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&cmd=llinkslib&id=16210666](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&cmd=llinkslib&id=16210666)

**Example**: Find information from clinicaltrials.gov for a PMID.

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&cmd=llinkslib&id=16210666&holding=CTgov](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=pubmed&cmd=llinkslib&id=16210666&holding=CTgov)
<br>
 ### Optional Parameters – Dates

These parameters only function when  cmd  is set to neighbor  or neighbor_history  and  dbfrom  is  pubmed.
datetype

Type of date used to limit a link operation. The allowed values vary between Entrez databases, but common values are 'mdat' (modification date), 'pdat' (publication date) and 'edat' (Entrez date). Generally, an Entrez database will have only two allowed values for datetype.
<br>
**reldate**

When reldate is set to an integer n, ELink returns only those items that have a date specified by datetype within the last n days.
<br>
**mindate, maxdate**

Date range used to limit a link operation by the date specified by datetype. These two parameters (mindate, maxdate) must be used together to specify an arbitrary date range. The general date format is YYYY/MM/DD, and these variants are also allowed: YYYY, YYYY/MM.

