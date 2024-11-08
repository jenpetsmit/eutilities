# Access E-utilities via Internet Browser

To use any internet browser as your E-utilities API interface, build a URL comprised of the following;
  * Base path
  * E-utility
  * [Required](eutilties/parameters.md#required) and [optional](eutilties/parameters.md#optional) parameters

Using the [E-utilties Base Path](./about.md#api-base-path):

 https://eutils.ncbi.nlm.nih.gov/entrez/eutils/{   }.fcgi? 

 1. Replace the brackets with the name of an E-utility 
 
For example: https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi? 

 2. Add parameters after the question mark.
  * For more than one parameter, add an ampersand (&) to add
  * For more than one UID, add a comman to separate IDs

**Examples**
Copy and paste one of the examples in your browser search field.

**eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?term=mouse&db=sra**

**eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?db=protein&id=6678417,9507199,28558982,28558984,28558988,28558990**

3. Copy the base path including the E-utility and parameters into any internet browser.

## Reponse
An XML formatted reponse returns.

Returns have a default limit of a maximum of 20. To change the default limit see _retmax_ on the [Parameter's Page](eutilities/parameters.md#retmax)
  
