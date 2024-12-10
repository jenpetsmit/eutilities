# E-Utilities Quick Start

E-Utilities Quick Start demonstrates how to use the most popular/common E-Utilities and a few of their parameters via your internet browser.

 

This quick start introduces you to using the most common E-Utilities. See [E-utilities](eutils/eutils_home.md).for a complete list of E-utilities with advanced options:

- **[ESearch](#esearch)** for Searching    
- **[ESummary](#esummary)** for downloading summaries of database records
- **[Efetch](#efetch)** for returning full data records
- **[Elink](#elink)** for returning data linked between two databases


---

 
## ESearch  

You can do a basic search using a simple query in your internet browser.

### Steps:
1. **Start with the base URL**  
   All E-utility queries begin with the following URL:  
   `https://eutils.ncbi.nlm.nih.gov/entrez/eutils/{ }.fcgi?`

2. **Replace the brackets with the search E-utility `esearch`**  
   Example:  
   `https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?`

3. **Add required parameters to the base URL**  
   - If more than one, join with `&`
   - Do not include spaces

For **Esearch**, the required parameters are:

| **Parameter** | **Description**                     | **Example**          |
|---------------|-------------------------------------|----------------------|
| `db`          | Entrez database you want to search | `db=pubmed`         |
| `term`        | Word you want to search for         | `term=asthma`       |

**Example URL:**  
`https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&term=asthma`

- Click the URL or  
- Copy and paste into any internet browser and press the Enter key.

### Results:
- **ESearch** returns a list of UIDs displayed in the internet browser.  
- By default, the maximum number of results is limited to 20.  


##  ESummary  

You can create a query for a document summary of each UID using the **ESummary** E-utility in your internet browser.

`esummary.fcgi?db=<database>&id=<uid_list>`

**Input**: List of UIDs (&id); Entrez database (&db)

**Output**: XML DocSums

**Example**: Download DocSums for these protein GIs: 6678417,9507199,28558982,28558984,28558988,28558990

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?db=protein&id=6678417,9507199,28558982,28558984,28558988,28558990](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?db=protein&id=6678417,9507199,28558982,28558984,28558988,28558990)



## Efetch  

Returns full records in a variety of formats, not just XML. 

`efetch.fcgi?db={database}&id={uid_list}&rettype={retrieval_type}&retmode={retrieval_mode}`

For **Efetch**, the required parameters are:

| **Parameter** | **Description**                     | **Example**          |
|---------------|-------------------------------------|----------------------|
| `db`          | Entrez database you want to search | `db=pubmed`         |
 

**Input**: List of UIDs (&id); Entrez database (&db); Retrieval type (&rettype); Retrieval mode (&retmode)

**Output**: Formatted data records as specified

**Example**: Download nuccore GIs 34577062 and 24475906 in FASTA format

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nuccore&id=34577062,24475906&rettype=fasta&retmode=text](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nuccore&id=34577062,24475906&rettype=fasta&retmode=text)



##  Elink 

Get a list of UIDs that are in the Source Database and linked to the Destination Database (Linked UIDs).

`elink.fcgi?dbfrom={source_db}&db={destination_db}&id={uid_list}`

For **Elink**, the required parameters are:

| **Parameter** | **Description**                     | **Example**          |
|---------------|-------------------------------------|----------------------|
| `db`          | Entrez database you want to search | `db=pubmed`         | 
| `dbfrom`      | Entrez database containing the input UIDs  | `dbfrom=protien`|
| `id`          | UID list                                    | `id=34577062,24475906 |

[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=nuccore&db=gene&id=34577062,24475906](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?dbfrom=nuccore&db=gene&id=34577062,24475906)
 
