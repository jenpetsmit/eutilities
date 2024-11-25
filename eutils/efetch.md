# EFetch

## Basic Downloading   

```efetch.fcgi?db={database}&id={uid_list}&rettype={retrieval_type}&retmode={retrieval_mode}```

**Input:** List of UIDs (&id); Entrez database (&db); Retrieval type (&rettype); Retrieval mode (&retmode)

**Output:**  Given a list of UIDs or a set of UIDs stored on the Entrez History server, returns formatted data records

**Example:** Download nuccore GIs 34577062 and 24475906 in FASTA format

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nuccore&id=34577062,24475906&rettype=fasta&retmode=text```
 
Returns full records in a variety of formats, not just XML. 

Use the ```&rettype = fasta & retmode = text```    to indicate in which format you want the response. 

For example:

```FASTA: 	&rettype = fasta & retmode = text```  

PubMed abstract: 	```&db=pubmed&rettype=abstract&retmode=text```

 ## Required Parameters

 id  
 UID list. 
 
Either a single UID or a comma-delimited list of UIDs may be provided. All of the UIDs must be specified by db. There is no set maximum for the number of UIDs that can be passed to EFetch, but if more than about 200 UIDs are to be provided, the request should be made using the HTTP POST method.  **[add link here]**

For sequence databases (nuccore, popset, protein), the UID list may be a mixed list of GI numbers and accession.version identifiers.

```efetch.fcgi?db=pubmed&id=19393038,30242208,29453458```

```efetch.fcgi?db=protein&id=15718680,NP_001098858.1,119703751```

**Special note for sequence databases**

NCBI is no longer assigning GI numbers to a growing number of new sequence records. As such, these records are not indexed in Entrez, and so cannot be retrieved using ESearch or ESummary, and have no Entrez links accessible by ELink. EFetch can retrieve these records by including their accession.version identifier in the id parameter.

 
## Required Parameters – Used only when input is from the **Entrez History server**

**query_key**

Query key. This integer specifies which of the UID lists attached to the given Web Environment will be used as input to EFetch. Query keys are obtained from the output of previous ESearch, EPost or ELInk calls. The query_key parameter must be used in conjunction with WebEnv.

**WebEnv**

Web Environment. This parameter specifies the Web Environment that contains the UID list to be provided as input to EFetch. Usually this WebEnv value is obtained from the output of a previous ESearch, EPost or ELink call. The WebEnv parameter must be used in conjunction with query_key.
efetch.fcgi?db=protein&query_key={key}&WebEnv={webenv string}

##  Optional Parameters – Retrieval

**rettype**

Retrieval type. This parameter specifies the record view returned, such as Abstract or MEDLINE from PubMed, or GenPept or FASTA from protein. Please see Table 1 for a full list of allowed values for each database.

**retstart**

Sequential index of the first record to be retrieved (default=0, corresponding to the first record of the entire set). This parameter can be used in conjunction with retmax to download an arbitrary subset of records from the input set.

**retmax**

Total number of records from the input set to be retrieved, up to a maximum of 10,000. Optionally, for a large set the value of retstart can be iterated while holding retmax constant, thereby downloading the entire set in batches of size retmax.

**retmode**

Retrieval mode. This parameter specifies the data format of the records returned, such as plain text, HMTL or XML. See Table 1 for a full list of allowed values for each database.
 
**Table 1: EFetch: Valid values of “&retmode” and “&rettype” (null = empty string)**
| Record Type                                    | &rettype              | &retmode               |
|------------------------------------------------|-----------------------|------------------------|
| **All Databases**                              |                       |                        |
| &nbsp;&nbsp;&nbsp;&nbsp;Document summary                               | docsum                | xml (default)          |
|&nbsp;&nbsp;&nbsp;&nbsp; List of UIDs in XML                            | uilist                | xml                    |
| &nbsp;&nbsp;&nbsp;&nbsp;List of UIDs in plain text                     | uilist                | text                   |
| **db = bioproject**                            |                       |                        |
|&nbsp;&nbsp;&nbsp;&nbsp; Full record XML                                | xml, default          | xml (default)          |
| **db = biosample**                             |                       |                        |
| &nbsp;&nbsp;&nbsp;&nbsp;Full record XML                                | full, default         | xml (default)          |
| &nbsp;&nbsp;&nbsp;&nbsp;Full record text                               | full, default         | text                   |
| **db = gds**                                   |                       |                        |
| &nbsp;&nbsp;&nbsp;&nbsp;Summary                                        | summary, default      | text (default)         |
| **db = gene**                                  |                       |                        |
| &nbsp;&nbsp;&nbsp;&nbsp;text ASN.1                                     | null                  | asn.1 (default)        |
| &nbsp;&nbsp;&nbsp;&nbsp;XML                                            | null                  | xml                    |
| &nbsp;&nbsp;&nbsp;&nbsp;Gene table                                     | gene_table            | text                   |
| **db = homologene**                            |                       |                        |
| &nbsp;&nbsp;&nbsp;&nbsp;text ASN.1                                     | null                  | asn.1 (default)        |
| &nbsp;&nbsp;&nbsp;&nbsp;XML                                            | null                  | xml                    |
| &nbsp;&nbsp;&nbsp;&nbsp;Alignment scores                               | alignmentscores       | text                   |
| &nbsp;&nbsp;&nbsp;&nbsp;FASTA                                          | fasta                 | text                   |
| &nbsp;&nbsp;&nbsp;&nbsp;HomoloGene                                     | homologene            | text                   |
| **db = mesh**                                  |                       |                        |
| &nbsp;&nbsp;&nbsp;&nbsp;Full record                                    | full (default)        | text (default)         |
| **db = nlmcatalog**                            |                       |                        |
|&nbsp;&nbsp;&nbsp;&nbsp; Full record                                    | null                  | text (default)         |
| &nbsp;&nbsp;&nbsp;&nbsp;XML                                            | null                  | xml                    |
| **db = nuccore, protein or popset**            |                       |                        |
| &nbsp;&nbsp;&nbsp;&nbsp;text ASN.1                                     | null                  | text (default)         |
| &nbsp;&nbsp;&nbsp;&nbsp;binary ASN.1                    
| **Additional options for db = nuccore or popset** |                       |                        |
|&nbsp;&nbsp;&nbsp;&nbsp; GenBank flat file                              | gb                    | text                   |
|&nbsp;&nbsp;&nbsp;&nbsp; GBSeq XML                                      | gb                    | xml                    |
|&nbsp;&nbsp;&nbsp;&nbsp;INSDSeq XML                                    | gbc                   | xml                    |
| **Additional option for db = nuccore and protein** |                       |                        |
| &nbsp;&nbsp;&nbsp;&nbsp;Feature table                                  | ft                    | text                   |
| **Additional option for db = nuccore**         |                       |                        |
| &nbsp;&nbsp;&nbsp;&nbsp;GenBank flat file with full sequence (contigs) | gbwithparts           | text                   |
|&nbsp;&nbsp;&nbsp;&nbsp; CDS nucleotide FASTA                           | fasta_cds_na          | text                   |
|&nbsp;&nbsp;&nbsp;&nbsp; CDS protein FASTA                              | fasta_cds_aa          | text                   |
| **Additional options for db = protein**        |                       |                        |
| &nbsp;&nbsp;&nbsp;&nbsp;GenPept flat file                              | gp                    | text                   |
| &nbsp;&nbsp;&nbsp;&nbsp;GBSeq XML                                      | gp                    | xml                    |
| &nbsp;&nbsp;&nbsp;&nbsp;INSDSeq XML                                    | gpc                   | xml                    |
|&nbsp;&nbsp;&nbsp;&nbsp; Identical Protein XML                          | ipg                   | xml                    |
| **db = pmc**                                   |                       |                        |
|&nbsp;&nbsp;&nbsp;&nbsp; XML                                            | null                  | xml (default)          |
| &nbsp;&nbsp;&nbsp;&nbsp;MEDLINE                                        | medline               | text                   |
| **db = pubmed**                                |                       |                        |
|&nbsp;&nbsp;&nbsp;&nbsp; XML                                            | null                  | xml (default)          |
|&nbsp;&nbsp;&nbsp;&nbsp; MEDLINE                                        | medline               | text                   |
| &nbsp;&nbsp;&nbsp;&nbsp;PMID list                                      | uilist                | text                   |
| &nbsp;&nbsp;&nbsp;&nbsp;Abstract                                       | abstract              | text                   |
| **db = sequences**                             |                       |                        |
| &nbsp;&nbsp;&nbsp;&nbsp;text ASN.1                                     | null                  | text (default)         |
| &nbsp;&nbsp;&nbsp;&nbsp;Accession number(s)                            | acc                   | text                   |
| &nbsp;&nbsp;&nbsp;&nbsp;FASTA                                          | fasta                 | text                   |
| &nbsp;&nbsp;&nbsp;&nbsp;SeqID string                                   | seqid                 | text                   |
| **db = snp**                                   |                       |                        |
|&nbsp;&nbsp;&nbsp;&nbsp; text ASN.1                                     | null                  | asn.1 (default)        |
| &nbsp;&nbsp;&nbsp;&nbsp;XML                                            | null                  | xml                    |
|&nbsp;&nbsp;&nbsp;&nbsp; Flat file                                      | flt                   | text                   |
|&nbsp;&nbsp;&nbsp;&nbsp; FASTA                                          | fasta                 | text                   |
| &nbsp;&nbsp;&nbsp;&nbsp;RS Cluster report                              | rsr                   | text                   |
| &nbsp;&nbsp;&nbsp;&nbsp;SS Exemplar list                               | ssexemplar            | text                   |
| &nbsp;&nbsp;&nbsp;&nbsp;Chromosome report                              | chr                   | text                   |
| &nbsp;&nbsp;&nbsp;&nbsp;Summary                                        | docset                | text                   |
| &nbsp;&nbsp;&nbsp;&nbsp;UID list                                       | uilist                | text or xml            |
| **db = sra**                                   |                       |                        |
| &nbsp;&nbsp;&nbsp;&nbsp;XML                                            | full (default)        | xml (default)          |
| **db = taxonomy**                              |                       |                        |
| &nbsp;&nbsp;&nbsp;&nbsp;XML                                            | null                  | xml (default)          |
| &nbsp;&nbsp;&nbsp;&nbsp;TaxID list                                     | uilist                | text or xml            |
| **db = clinvar**                               |                       |                        |
| &nbsp;&nbsp;&nbsp;&nbsp;ClinVar Set                                    | clinvarset           | xml (default)          |
|&nbsp;&nbsp;&nbsp;&nbsp; UID list                                       | uilist                | text or xml            |
| **db = gtr**                                    |                       |                        |
| &nbsp;&nbsp;&nbsp;&nbsp;GTR Test Report                                | gtracc                | xml (default)          |

## Optional Parameters for Sequence Databases
**strand**

Strand of DNA to retrieve. Available values are "1" for the plus strand and "2" for the minus strand.

**seq_start**

First sequence base to retrieve. The value should be the integer coordinate of the first desired base, with "1" representing the first base of the sequence.

**seq_stop**

Last sequence base to retrieve. The value should be the integer coordinate of the last desired base, with "1" representing the first base of the sequence.

**complexity**

Data content to return. Many sequence records are part of a larger data structure or "blob", and the complexity parameter determines how much of that blob to return. For example, an mRNA may be stored together with its protein product. The available values are as follows:

| Value of complexity | Data returned for each requested GI  |
| --- | --- |
| 0 | entire blob |
| 1 | bioseq |
| 2 | minimal bioseq-set |
| 3 | minimal nuc-prot |
| 4 | minimal pub-set |

**[CAN WE REPLACE 'BLOB' WITH SOMETHING MORE DISTINCT?]**

### Examples

#### PubMed
Fetch PMIDs 17284678 and 9997 as text abstracts:

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=pubmed&id=17284678,9997&retmode=text&rettype=abstract ```

Fetch PMIDs in XML:

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=pubmed&id=11748933,11700088&retmode=xml```

#### PubMed Central
Fetch XML for PubMed Central ID 212403:

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=pmc&id=212403 ```

#### Nucleotide/Nuccore
 Fetch the first 100 bases of the plus strand of GI 21614549 in FASTA format:
 
```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nuccore&id=21614549&strand=1&seq_start=1&seq_stop=100&rettype=fasta&retmode=text ```

 Fetch the first 100 bases of the minus strand of GI 21614549 in FASTA format:
 
```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nuccore&id=21614549&strand=2&seq_start=1&seq_stop=100&rettype=fasta&retmode=text ```


Fetch the nuc-prot object for GI 21614549:

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nuccore&id=21614549&complexity=3 ```


Fetch the full ASN.1 record for GI 5:

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nucleotide&id=5 ```


Fetch FASTA for GI 5:

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nucleotide&id=5&rettype=fasta ```


Fetch the GenBank flat file for GI 5:

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nucleotide&id=5&rettype=gb ```


Fetch GBSeqXML for GI 5:

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nucleotide&id=5&rettype=gb&retmode=xml ```


Fetch TinySeqXML for GI 5:

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nucleotide&id=5&rettype=fasta&retmode=xml ```


 
#### Protein
Fetch the GenPept flat file for GI 8:

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=protein&id=8&rettype=gp ```


Fetch GBSeqXML for GI 8:

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=protein&id=8&rettype=gp&retmode=xml ```


####  Sequences
Fetch FASTA for a transcript and its protein product (GIs 312836839 and 34577063)

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=sequences&id=312836839,34577063&rettype=fasta&retmode=text ```


#### Gene
Fetch full XML record for Gene ID 2:

```[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=gene&id=2&retmode=xml](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=gene&id=2&retmode=xml) ```


