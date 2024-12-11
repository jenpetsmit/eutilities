# Access E-utility APIs Using Command Line

Use Entrez Direct programs to work on large sets of data. They manage many technical details behind the scenes (avoiding the learning curve normally required for E-Utilities programming). Intermediate results are either saved on the Entrez history server or instantiated in a hidden message. 

## API Key
 Although not required, for best performance, [obtain an API Key from NCBI](./access/api_key.md), and place the following line in your .bash_profile and .zshrc configuration files:

  ```export NCBI_API_KEY=unique_api_key```

## Installation
EDirect runs on Unix, Linux, and Macintosh computers, and under the Cygwin Unix-emulation environment on Windows PCs.

To install the EDirect software: 
1.	Open a terminal window and copy and paste one of the following two commands:
   
`sh -c "$(curl -fsSL https://ftp.ncbi.nlm.nih.gov/entrez/entrezdirect/install-edirect.sh)`

`sh -c "$(wget -q https://ftp.ncbi.nlm.nih.gov/entrez/entrezdirect/install-edirect.sh -O -)`
  
An edirect folder with several scripts and precompiled programs is added to your home directory. 

As a convenience, the installation process offers to run the PATH update command for you. 

`echo "export PATH=\$HOME/edirect:\$PATH" >> $HOME/.bash_profile`
  
If you want to automatically update the export PATH:

2.	Answer **y** and press the **Return** key
3.	If the PATH is already set correctly, or if you prefer to make any editing changes manually, just press **Return**.

 
 
#### Minimizing the Number of Requests   **FIX OR MOVE THIS LATER**
If a task requires searching for and/or downloading a large number of records,  use the Entrez History (server? does this go here?) to upload and retrieve these records in batches rather than using separate requests for each record. 
Please refer to Application 3 in Chapter 3 for an example. Many thousands of IDs can be uploaded using a single EPost request, and several hundred records can be downloaded using one EFetch request.


# Using EDirect
Search terms are entered as command-line arguments. Individual operations connect with Unix pipes to construct multi-step queries for you. Selected records are retrieved in a variety of formats.

 ## ESearch   
Esearch performs a new search using terms in indexed fields. **SHOULD WE INCLUDE A LIST FIELDS HAVE BEEN INDEXED?** 

To use ESearch, follow the structure of this example:

`esearch -db pubmed -query "selective serotonin reuptake inhibitor"`

Search terms can also be qualified with a bracketed field name to match within the specified index, for example:

`esearch -db nuccore -query "insulin [PROT] AND rodents [ORGN]"`

**Table: Required Fields for ESearch**    **<-- REQUIRED FIELDS ARE THE SAME FOR COMMAND LINE AND BROWSER AND PROB API -->**

| common name | argument |  example |
| --- | ---  | --- |
| database | -db | -db nucore |
| search term | -query | -query "insulin [PROT] AND rodents [ORGN]" |



( **DO WE NEED TO INCLUDE THIS:**  For PubMed, without field qualifiers, the server uses automatic term mapping to compose a search strategy by translating the supplied query?)
 


## ELink 
ELink looks up precomputed neighbors within a database or finds associated records in other databases:

  `elink -related`

  `elink -target gene`
  
ELink also connects to the NIH Open Citation Collection dataset to find publications that cite the selected PubMed articles, or to follow the reference lists of PubMed records:

  `elink -cited`

 `elink -cites`

 ## EFilter
Efilter limits the results of a previous query, with shortcuts that can also be used in esearch:

  `eFilter -molecule genomic -location chloroplast -country sweden -mindate 1985`
Efetch downloads selected records or reports in a style designated by ‑format:

  `efetch -format abstract`
There is no need to use a script to loop over records in small groups, or write code to retry after a transient network or server failure, or add a time delay between requests. All of those features are already built into the EDirect commands.

## Constructing Multi-Step Queries
EDirect allows individual operations to be described separately, combining them into a multi-step query by using the vertical bar ("|") Unix pipe symbol:

  `esearch -db pubmed -query "tn3 transposition immunity" | efetch -format medline`
  
### Writing Commands on Multiple Lines
A query can be continued on the next line by typing the backslash ("\") Unix escape character immediately before pressing the Return key.

  `esearch -db pubmed -query "opsin gene conversion" | \`
  
Continuing the query looks up precomputed neighbors of the original papers, next links to all protein sequences published in the related articles, then limits those to the rodent division of GenBank, and finally retrieves the records in FASTA format:

```
  elink -related | \
  elink -target protein | \
  efilter -division rod | \
  efetch -format fasta
```

In most modern versions of Unix, the vertical bar pipe symbol also allows the query to continue on the next line, without the need for an additional backslash.

## Construct Multi-Step Queries
EDirect allows individual operations to be described separately. Combine them into a multi-step query by using the vertical bar ("|") Unix pipe symbol:

  ```esearch -db pubmed -query "tn3 transposition immunity" | efetch -format medline```

## Writing Commands on Multiple Lines
A query can be continued on the next line by typing the backslash ("\") Unix escape character immediately before pressing the **Return** key, for example:

  ```esearch -db pubmed -query "opsin gene conversion" | \```
  
These lines:

  elink -related | \
  elink -target protein | \
  efilter -division rod | \
  efetch -format fasta

do the following in order: 
 * **elink -related**  looks up precomputed neighbors of the original papers. 
 * **elink -target protein**  links to all protein sequences published in the related articles.
 * **Efilter -division rod** limits the related artcles to the rodent division of GenBank. 
 * **efetch -format fasta** retrieves the records in FASTA format:

In most modern versions of Unix, the vertical bar pipe symbol also allows the query to continue to the next line without the need for an additional backslash.



# very long page of examples available Here 

## Probably need to break them down into subpages maybe?

https://www.ncbi.nlm.nih.gov/books/NBK179288/ 
