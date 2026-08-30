# Search BOLD for taxonomy data by BOLD ID.

Search BOLD for taxonomy data by BOLD ID.

## Usage

``` r
bold_tax_id2(
  id,
  dataTypes = "basic",
  includeTree = FALSE,
  response = FALSE,
  ...
)
```

## Arguments

- id:

  (integer\|numeric\|character) One or more BOLD taxonomic identifiers.
  required.

- dataTypes:

  (character) One or more BOLD data types: 'basic', 'stats', 'geo',
  'images'/'img', 'sequencinglabs'/'labs', 'depository'/'depo',
  'thirdparty'/'wiki' or 'all' (default: 'basic'). Specifies the
  information that will be returned, see details.

- includeTree:

  (logical) If `TRUE` (default: `FALSE`), returns the information for
  parent taxa as well as the specified taxon, see details.

- response:

  (logical) Default : FALSE. If TRUE, returns the object from the Curl
  call. Useful for debugging and getting more detailed info on the API
  call.

- ...:

  Further args passed on to
  [`crul::verb-GET`](https://docs.ropensci.org/crul/reference/verb-GET.html),
  main purpose being curl debugging

## dataTypes

"basic" returns basic taxonomy info: includes taxid, taxon name, tax
rank, tax division, parent taxid, parent taxon name. "stats" returns
specimen and sequence statistics: includes public species count, public
BIN count, public marker counts, public record count, specimen count,
sequenced specimen count, barcode specimen count, species count, barcode
species count. "geo" returns collection site information: includes
country, collection site map. "images" returns specimen images: includes
copyright information, image URL, image metadata. "sequencinglabs"
returns sequencing labs: includes lab name, record count. "depository"
returns specimen depositories: includes depository name, record count.
"thirdparty" returns information from third parties: includes
wikipedia_summary summary, wikipedia_summary URL. "all" returns all
information: identical to specifying all data types at once.

## includeTree

When `includeTree` is set to true, for the `dataTypes` other than
'basic' the information of the parent taxa are identified by their
taxonomic id only. To get their ranks and names too, make sure 'basic'
is in `dataTypes`.

## References

http://v4.boldsystems.org/index.php/resources/api?type=taxonomy

## See also

[`bold_tax_name`](https://docs.ropensci.org/bold/reference/bold_tax_name.md),
[`bold_get_attr`](https://docs.ropensci.org/bold/reference/bold_get_attr.md),
[`bold_get_errors`](https://docs.ropensci.org/bold/reference/bold_get_attr.md),
[`bold_get_params`](https://docs.ropensci.org/bold/reference/bold_get_attr.md)

## Examples

``` r
if (FALSE) { # \dontrun{
bold_tax_id2(id = 88899)
bold_tax_id2(id = 88899, includeTree = TRUE)
bold_tax_id2(id = 88899, includeTree = TRUE, dataTypes = "stats")
bold_tax_id2(id = c(88899, 125295))

## dataTypes parameter
bold_tax_id2(id = 88899, dataTypes = "basic")
bold_tax_id2(id = 88899, dataTypes = "stats")
bold_tax_id2(id = 88899, dataTypes = "images")
bold_tax_id2(id = 88899, dataTypes = "geo")
bold_tax_id2(id = 88899, dataTypes = "sequencinglabs")
bold_tax_id2(id = 88899, dataTypes = "depository")
bold_tax_id2(id = 88899, dataTypes = "thirdparty")
bold_tax_id2(id = 88899, dataTypes = "all")
bold_tax_id2(id = c(88899, 125295), dataTypes = c("basic", "geo"))
bold_tax_id2(id = c(88899, 125295), dataTypes = c("basic", "stats", "images"))

## Passing in NA
bold_tax_id2(id = NA)
bold_tax_id2(id = c(88899, 125295, NA))

## get http response object only
bold_tax_id2(id = 88899, response = TRUE)
bold_tax_id2(id = c(88899, 125295), response = TRUE)

## curl debugging
bold_tax_id2(id = 88899, verbose = TRUE)
} # }
```
