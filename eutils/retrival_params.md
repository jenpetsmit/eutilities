# Retrival Parameters


**retstart**
  * Sequential index of the first UID in the retrieved set to be shown in the XML output (default=0, corresponding to the first record of the entire set). This parameter can be used in conjunction with retmax to download an arbitrary subset of UIDs retrieved from a search.

**retmax**
  * Total number of UIDs from the retrieved set to be shown in the XML output (default=20). By default, ESearch only includes the first 20 UIDs retrieved in the XML output. If usehistory is set to 'y', the remainder of the retrieved set will be stored on the History server; otherwise these UIDs are lost. Increasing retmax allows more of the retrieved UIDs to be included in the XML output, up to a maximum of 10,000 records.

  * To retrieve more than 10,000 UIDs from databases other than PubMed, submit multiple esearch requests while incrementing the value of retstart (see Application 3). For PubMed, ESearch can only retrieve the first 10,000 records matching the query. To obtain more than 10,000 PubMed records, consider using <EDirect> that contains additional logic to batch PubMed search results automatically so that an arbitrary number can be retrieved.

**rettype**
  * There are two allowed values for ESearch: 'uilist' (default), which displays the standard XML output, and 'count', which displays only the <Count> tag.

**retmode**
  * Determines the format of the returned output. The default value is ‘xml’ for ESearch XML, but ‘json’ is also supported to return output in JSON format.

**sort**
  * Specifies the method used to sort UIDs in the ESearch output. The available values vary by database (db) and may be found in the Display Settings menu on an Entrez search results page. If usehistory is set to ‘y’, the UIDs are loaded onto the History Server in the specified sort order and will be retrieved in that order by ESummary or EFetch. Example values are ‘relevance’ and ‘name’ for Gene. Users should be aware that the default value of sort varies from one database to another, and that the default value used by ESearch for a given database may differ from that used on NCBI web search pages.

Values of sort for PubMed are as follows:

  * _pub_date_ – descending sort by publication date
  * _Author_ – ascending sort by first author
  * _JournalNam_e – ascending sort by journal name
  * _relevance_ – default sort order, (“Best Match”) on web PubMed

**field**
  * The entire search term will be limited to the specified Entrez field. The following two URLs are equivalent:

esearch.fcgi?db=pubmed&term=asthma&field=title

esearch.fcgi?db=pubmed&term=asthma[title]

**idtype**
  * Specifies the type of identifier to return for sequence databases (nuccore, popset, protein). By default, ESearch returns GI numbers in its output. If idtype is set to ‘acc’, ESearch will return accession.version identifiers rather than GI numbers.
