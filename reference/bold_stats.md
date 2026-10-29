# Get BOLD stats

Get BOLD stats

## Usage

``` r
bold_stats(
  taxon = NULL,
  ids = NULL,
  bin = NULL,
  container = NULL,
  institutions = NULL,
  researchers = NULL,
  geo = NULL,
  dataType = "drill_down",
  response = FALSE,
  simplify = FALSE,
  ...
)
```

## Arguments

- taxon:

  (character) One or more taxonomic name. Optional.

- ids:

  (character\|integer\|numeric) One or more IDs. Optional. IDs include
  Sample IDs, Process IDs, Museum IDs and Field IDs.

- bin:

  (character) One or more Barcode Index Number URI. Optional.

- container:

  (character) One or more project codes or dataset codes. Optional.

- institutions:

  (character) One or more institution's name. Optional. Institutions are
  the Specimen Storing Site.

- researchers:

  (character) One or more researcher names. Optional. Include collectors
  and specimen identifiers.

- geo:

  (character) One or more geographic sites. Includes countries and
  province/states.

- dataType:

  (character) one of "drill_down"(default) or "overview". "drill_down":
  a detailed summary of information which provides record counts by
  BINs, Countries, Storing Institutions, Orders, Families, Genus,
  Species. "overview": the total record counts of BINs, Countries,
  Storing Institutions, Orders, Families, Genus, Species. The record
  counts include all gene markers, not only COI. To see the drill down
  of markers use
  [`bold_tax_id2`](https://docs.ropensci.org/bold/reference/bold_tax_id2.md)
  with "stats" as `dataTypes`.

- response:

  (logical) Default : FALSE. If TRUE, returns the object from the Curl
  call. Useful for debugging and getting more detailed info on the API
  call.

- simplify:

  (logical) whether the returned list should be simplified to a
  data.frame. See Details.

- ...:

  Further args passed on to
  [`crul::verb-GET`](https://docs.ropensci.org/crul/reference/verb-GET.html),
  main purpose being curl debugging

## Value

By default, returns a nested list with the number of total records, the
number of records with a species name, then for each of bins, countries,
depositories, order, family, genus and species, the total count and the
drill down of the records by up to 10 entities of that category. If
`simplify` is set to TRUE, returns a list of length 2 : the overview
data (number of total records, the number of records with a species
name, and the total counts) simplified as a data.frame of 1 row and 9
columns and the drill_down data simplified to a one level list of
data.frame. When `dataType` is set to "overview", returns a nested list
with the number of total records, the number of records with a species
name, and the total count for each of bins, countries, depositories,
order, family, genus and species. If `simplify` is set to TRUE, returns
a data.frame of 1 row and 9 columns.

## References

http://v4.boldsystems.org/index.php/resources/api?type=webservices

## Examples

``` r
if (FALSE) { # \dontrun{
x <- bold_stats(taxon='Osmia')
x$total_records
x$records_with_species_name
x$bins
x$countries
x$depositories
x$order
x$family
x$genus
x$species

# just get all counts
lapply(Filter(is.list, x), `[[`, "count")

bold_stats(taxon='Osmia', dataType = "overview", simplified = TRUE)

x <- bold_stats(taxon='Osmia', simplified = TRUE)
x$overview
x$drill_down

res <- bold_stats(taxon='Osmia', response=TRUE)
res$url
res$status_code
res$response_headers

# More than 1 can be given for all search parameters

## curl debugging
### These examples below take a long time, so you can set a timeout so that
### it stops by X sec
bold_stats(taxon='Osmia', verbose = TRUE)
# bold_stats(geo='Costa Rica', timeout_ms = 6)
} # }
```
