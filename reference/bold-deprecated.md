# Deprecated functions in package bold.

The functions listed below are deprecated and will be defunct in the
near future. When possible, alternative functions with similar
functionality are also mentioned. Help pages for deprecated functions
are available at `help("<function>-deprecated")`.

## Usage

``` r
bold_identify_parents(
  x,
  wide = FALSE,
  taxid = NULL,
  taxon = NULL,
  tax_rank = NULL,
  tax_division = NULL,
  parentid = NULL,
  parentname = NULL,
  taxonrep = NULL,
  specimenrecords = NULL,
  ...
)

bold_tax_id(
  id,
  dataTypes = "basic",
  includeTree = FALSE,
  response = FALSE,
  ...
)
```

## Value

a list of the same length as the input

## Details

DEPRECATED. See
[`bold_identify_taxonomy`](https://docs.ropensci.org/bold/reference/bold_identify_taxonomy.md).
It's faster and gets the accurate taxonomy directly from the record of
the sequence.

This function gets unique set of taxonomic names from the input
data.frame, then queries
[`bold_tax_name`](https://docs.ropensci.org/bold/reference/bold_tax_name.md)
to get the taxonomic ID, passing it to `bold_tax_id` to get the parent
names, then attaches those to the input data.

Records in the input data that do not have matches for parent names
simply get NA values in the added columns.

## `bold_identify_parents`

For `bold_identify_parents`, use
[`bold_identify_taxonomy`](https://docs.ropensci.org/bold/reference/bold_identify_taxonomy.md).

## Filtering

The parameters `taxid`, `taxon`, `tax_rank`, `tax_division`, `parentid`,
`parentname`,`taxonrep`, and `specimenrecords` are not used in the
search sent to BOLD, but are used in filtering the data down to a subset
that is closer to the target you want. For all these parameters, you can
use regex strings since we use
[`grep`](https://rdrr.io/r/base/grep.html) internally to match.
Filtering narrows down to the set that matches your query, and removes
the rest. The data.frame that we filter on with these parameters
internally is the result of a call to the
[`bold_tax_name`](https://docs.ropensci.org/bold/reference/bold_tax_name.md)
function.

## wide vs long format

When `wide = FALSE` you get many rows for each record. Essentially, we
`cbind` the taxonomic classification onto the one row from the result of
[`bold_identify`](https://docs.ropensci.org/bold/reference/bold_identify.md),
giving as many rows as there are taxa in the taxonomic classification.

When `wide = TRUE` you get one row for each record - thus the dimensions
of the input data stay the same. For this option, we take just the rows
for taxonomic ID and name for each taxon in the taxonomic
classification, and name the columns by the taxon rank, so you get
`phylum` and `phylum_id`, and so on.

## `bold_tax_id`

For `bold_tax_id`, use
[`bold_tax_id2`](https://docs.ropensci.org/bold/reference/bold_tax_id2.md).

## References

http://v4.boldsystems.org/index.php/resources/api?type=taxonomy

## See also

[`bold_tax_name()`](https://docs.ropensci.org/bold/reference/bold_tax_name.md)

## Examples

``` r
if (FALSE) { # \dontrun{
df <- bold_identify(sequences = sequences$seq2)

# long format
out <- bold_identify_parents(df)
str(out)
head(out[[1]])

# wide format
out <- bold_identify_parents(df, wide = TRUE)
str(out)
head(out[[1]])

x <- bold_seq(taxon = "Satyrium")
out <- bold_identify(c(x[[1]]$sequence, x[[13]]$sequence))
res <- bold_identify_parents(out)
res

x <- bold_seq(taxon = 'Diplura')
out <- bold_identify(vapply(x, "[[", "", "sequence")[1:20])
res <- bold_identify_parents(out)
} # }
if (FALSE) { # \dontrun{
bold_tax_id(id = 88899)
bold_tax_id(id = 88899, includeTree = TRUE)
bold_tax_id(id = 88899, includeTree = TRUE, dataTypes = "stats")
bold_tax_id(id = c(88899,125295))

## dataTypes parameters
bold_tax_id(id = 88899, dataTypes = "basic")
bold_tax_id(id = 88899, dataTypes = "stats")
bold_tax_id(id = 88899, dataTypes = "images")
bold_tax_id(id = 88899, dataTypes = "geo")
bold_tax_id(id = 88899, dataTypes = "sequencinglabs")
bold_tax_id(id = 88899, dataTypes = "depository")
bold_tax_id(id = c(88899, 125295), dataTypes = "geo")
bold_tax_id(id = c(88899, 125295), dataTypes = "images")

## Passing in NA
bold_tax_id(id = NA)
bold_tax_id(id = c(88899, 125295, NA))

## get http response object only
bold_tax_id(id = 88899, response=TRUE)
bold_tax_id(id = c(88899, 125295), response=TRUE)

## curl debugging
bold_tax_id(id = 88899, verbose = TRUE)
} # }
```
