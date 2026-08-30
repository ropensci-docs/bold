# Search BOLD for specimens.

Search BOLD for specimens.

## Usage

``` r
bold_specimens(
  taxon = NULL,
  ids = NULL,
  bin = NULL,
  container = NULL,
  institutions = NULL,
  researchers = NULL,
  geo = NULL,
  response = FALSE,
  format = "tsv",
  cleanData = FALSE,
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

- response:

  (logical) Default : FALSE. If TRUE, returns the object from the Curl
  call. Useful for debugging and getting more detailed info on the API
  call.

- format:

  (character) One of xml, json, tsv (default). tsv format gives back a
  data.frame object. xml gives back parsed XML as `xml_document` object.
  'json' (JavaScript Object Notation) and 'dwc' (Darwin Core Archive)
  are supported in theory, but the JSON can be malformed, so we don't
  support that here, and the DWC option actually returns TSV.

- cleanData:

  (logical) If `TRUE`, the cell values containing only duplicated values
  (ex : "COI-5P\|COI-5P\|COI-5P") will be reduce to one value ("COI-5P")
  and empty string will be change to NA. Default: `FALSE`

- ...:

  Further args passed on to
  [`crul::verb-GET`](https://docs.ropensci.org/crul/reference/verb-GET.html),
  main purpose being curl debugging

## Note

If using the `taxon` parameter with another parameter, if the `taxon`
isn't found in the public database, it will act as if no `taxon` was
specified and try to return all the data for the other specified
parameter. You can make sure that the `taxon` you're looking up has
public records with
[`bold_stats`](https://docs.ropensci.org/bold/reference/bold_stats.md).

## References

http://v4.boldsystems.org/index.php/resources/api?type=webservices

## Examples

``` r
if (FALSE) { # \dontrun{
bold_specimens(taxon='Osmia')
bold_specimens(taxon='Osmia', format='xml')
bold_specimens(taxon='Osmia', response=TRUE)
res <- bold_specimens(taxon='Osmia', format='xml', response=TRUE)
res$url
res$status_code
res$response_headers

# More than 1 can be given for all search parameters
bold_specimens(taxon=c('Coelioxys','Osmia'))

## curl debugging
### These examples below take a long time, so you can set a timeout so that
### it stops by X sec
head(bold_specimens(taxon='Osmia', verbose = TRUE))
# head(bold_specimens(geo='Costa Rica', timeout_ms = 6))
} # }
```
