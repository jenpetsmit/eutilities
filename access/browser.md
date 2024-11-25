# Access E-utilities via Internet Browser

 You can do a simple query in your internet browser: 
 
 1. Start all Entrez queries with the following base URL:
    
```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/```

 2.	Add an E-Utility plus “.fcgi?”
    
```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/E-Utility.fcgi?```
 •	See Table 1 for a list of E-Utilities with descriptions.

 3.	Add required and optional parameters

```https://eutils.ncbi.nlm.nih.gov/entrez/eutils/E_Utilitiy.fcgi?parameters```

 •	See Table 2 for a list of parameters with descriptions
 
Here is an example of a simple Entrez query. You can click or copy and paste the URL in an internet browser to see how browser-based access works:
[https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?db=pubmed&id=19393038](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?db=pubmed&id=19393038)


## 	Rules of Writing Entrez API URLs
This section provides guidance to writing Entrez API URLs regarding ASCII limits, spaces, and case.  For very long queries (more than several hundred characters long), consider using an HTTP POST call. 

**ASCII Rules**

URLs can only be sent over the Internet using the ASCII character-set. Some Entrez URLs contain characters outside the ASCII set, so those characters have to be encoded into a valid ASCII format.
For example, quotation marks (“) and the octothorpe (#) symbol  are not ASCII characters. See Table 3 for a list of non-ASCII characters commonly used in Entrez URLs and their encoded substitutions.

**Table 3: Non-ASCII characters commonly used in Entrez URLs and their encoded substitutions**
|  Non ASCII Characters | Common Names | Encoded Substitutions | Example |
| --- | --- | --- | --- | 
| " | Quotation Marks | %22 |  ENTER EXAMPLE HERE |
| # | Octothorpe/ Hashtag/Pound Sign | %23 |ENTER EXAMPLE HERE |
| OTHER ? | --- | --- | ENTER EXAMPLE HERE |

### ASCII Encoding Examples

Search term = #2 and “gene in genomic”                              <-  CAN WE CHANGE THE 2 TO 5?

Incorrect:  &term=#2+AND+"gene in genomic"[properties]               <-- THE BRACKETS ARE WAY CONFUSING

Correct:   &term=%232+AND+%22gene+in+genomic%22[properties]

**Use of Spaces**
Do not include spaces in the URLs, particularly in queries. If a space is required, use a plus sign (+) instead of a space:

Incorrect:  &id=352, 25125, 234
 
 Correct:   &id=352,25125,234

Incorrect:  &term=biomol mrna[properties] AND mouse[organism]

Correct:   &term=biomol+mrna[properties]+AND+mouse[organism]

**Use of Lower- and Upper-Case**

When constructing URLs for the E-utilities, use lowercase characters for all parameters except for the **WebEnv** parameter. 

## Reponse
An XML formatted reponse returns.

Returns have a default limit of a maximum of 20. To change the default limit see _retmax_ on the [Parameter's Page](eutilities/parameters.md#retmax)
  
