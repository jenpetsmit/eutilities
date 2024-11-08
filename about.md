# About E-utilities

For latest announcments, please visit the E-Utilities News page.

NCBI Entrez utilities (E-utiliies) are nine E-utilites, which represent the interface for the NCBI API. The E-utilties enable you to gather data from 40 NCBI databases covering a variety of biomedical data, including nucleotide and protein sequences, gene records, three-dimensional molecular structures, and the biomedical literature.   

Figure: The Relationship between the User and NCBI Databases with the list of E-utilites as the Interface

![Figure showing the relationship between the User and NCBI databases with the list of E-utilites as the Interface](eutilies/images/about/figure1.png)

## NCBI Databases
There are about 40 NCBI databases. The number changes as databases configuration improve. 
Database names have an abbreviated alias used with API Searches. 
For example:
•	PM – PubMed database UID prefix
•	C – PubChem Compound database UID prefix
•	MMDB -  Molecular Modeling Database 

### UID
The UID is an numeric key used to identify a record in an NCBI database. The combination of the database alias and UID DOES SOMETHING?

### Parameter
When you do not know the UIDs of the records you want, include parameters in your search to narrow the results. 
There are several types of parameters.

**The database parameter**
The most common parameter is db, which narrows the search to one database.
example: db=pubmed

**Data parameters**
**pdat**  | publication data
**reldate**  | days to be search relative to the current date.  reldate =1 is for the most recent date
**mindate** and maxdate are used togeteher to provide a date range. mindate=YYY/MM/DD or YYYY/MM&maxdate=YYYY/MM/DD or YYYY/MM








