# E-Utilities Quick Start

E-Utilities Quick Start demonstrates how to use the most popular/common E-Utilities and a few of their parameters via your internet browser.

For complete information, see [E-utilities API](https://www.ncbi.nlm.nih.gov/books/NBK25501/).

This quick start introduces you to using the five most common E-Utilities. See [E-Utilities](https://www.ncbi.nlm.nih.gov/books/NBK25500/) for a complete list of E-utilities with advanced options:

- **ESearch** for Searching
- **ESummary** for downloading summaries of database records
- **Efetch** for returning full data records
- **Elink** for returning data linked between two databases
- **Epost** for saving your search history and using that information in another E-utility

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
- To change the number of results or add other optional parameters, see [ESearch documentation](https://www.ncbi.nlm.nih.gov/books/NBK25499/).

---

##  ESummary  

You can create a query for a summary of each UID using the **ESummary** E-utility in your internet browser.

---



## C-3 Efetch (Include in Quick Start?)

---

## C-4 Elink (Quick Start Version)

Get a list of UIDs that are in the Source Database and linked to the Destination Database (Linked UIDs).

### Modes:
- **Batch mode**: Finds only one set of linked UIDs.  
  Example:  
