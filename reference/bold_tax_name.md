# Search BOLD for taxonomy data by taxonomic name

Search BOLD for taxonomy data by taxonomic name

## Usage

``` r
bold_tax_name(
  name,
  fuzzy = FALSE,
  response = FALSE,
  tax_division = NULL,
  tax_rank = NULL,
  ...
)
```

## Arguments

- name:

  (character) One or more scientific names. required.

- fuzzy:

  (logical) Whether to use fuzzy search or not (default: `FALSE`)

- response:

  (logical) Default : FALSE. If TRUE, returns the object from the Curl
  call. Useful for debugging and getting more detailed info on the API
  call.

- tax_division:

  (character) Taxonomic division to filter the results.

- tax_rank:

  (character) Taxonomic rank to filter the results.

- ...:

  Further args passed on to
  [`crul::verb-GET`](https://docs.ropensci.org/crul/reference/verb-GET.html),
  main purpose being curl debugging

## Details

The `dataTypes` parameter is not supported in this function. If you want
to use that parameter, get an ID from this function and pass it into
`bold_tax_id`, and then use the `dataTypes` parameter.

## Note

The column 'specimenrecords' in the returned object represents the
number of species records in BOLD's *Taxonomy Browser*, not the number
of records in the *Public Data Portal*. To know the amount of public
records available, use
[`bold_stats`](https://docs.ropensci.org/bold/reference/bold_stats.md).

## References

Taxonomy API:
http://v4.boldsystems.org/index.php/resources/api?type=taxonomy Taxonomy
Browser: https://www.boldsystems.org/index.php/TaxBrowser_Home Public
Data Portal:
https://www.boldsystems.org/index.php/Public_BINSearch?searchtype=records

## See also

[`bold_tax_id`](https://docs.ropensci.org/bold/reference/bold-deprecated.md),
[`bold_get_attr`](https://docs.ropensci.org/bold/reference/bold_get_attr.md),
[`bold_get_errors`](https://docs.ropensci.org/bold/reference/bold_get_attr.md),
[`bold_get_params`](https://docs.ropensci.org/bold/reference/bold_get_attr.md)

## Examples

``` r
if (FALSE) { # \dontrun{
bold_tax_name(name='Diplura')
bold_tax_name(name='Osmia')
bold_tax_name(name=c('Diplura','Osmia'))
bold_tax_name(name=c("Apis","Puma concolor","Pinus concolor"))
bold_tax_name(name='Diplur', fuzzy=TRUE)
bold_tax_name(name='Osm', fuzzy=TRUE)

## get http response object only
bold_tax_name(name='Diplura', response=TRUE)
bold_tax_name(name=c('Diplura','Osmia'), response=TRUE)

## Names with no data in BOLD database
bold_tax_name("Nasiaeshna pentacantha")
bold_tax_name(name = "Cordulegaster erronea")
bold_tax_name(name = "Cordulegaster erronea", response=TRUE)

## curl debugging
bold_tax_name(name='Diplura', verbose = TRUE)
} # }
```
