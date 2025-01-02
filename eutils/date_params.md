# Data Parameters

**datetype**
  * Type of date used to limit a search. The allowed values vary between Entrez databases, but common values are 'mdat' (modification date), 'pdat' (publication date) and 'edat' (Entrez date). Generally an Entrez database will have only two allowed values for datetype.

**reldate**
  * When reldate is set to an integer n, the search returns only those items that have a date specified by datetype within the last n days.

**mindate, maxdate**
  * Date range used to limit a search result by the date specified by datetype. These two parameters (mindate, maxdate) must be used together to specify an arbitrary date range. The general date format is YYYY/MM/DD. These variants are also allowed: YYYY, YYYY/MM.
