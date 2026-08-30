# Get BOLD specimen + sequence data.

Get BOLD specimen + sequence data.

## Usage

``` r
bold_seqspec(
  taxon = NULL,
  ids = NULL,
  bin = NULL,
  container = NULL,
  institutions = NULL,
  researchers = NULL,
  geo = NULL,
  marker = NULL,
  response = FALSE,
  format = "tsv",
  sepfasta = FALSE,
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

- marker:

  (character) Returns all records containing matching marker codes. See
  Details.

- response:

  (logical) Default : FALSE. If TRUE, returns the object from the Curl
  call. Useful for debugging and getting more detailed info on the API
  call.

- format:

  (character) One of xml or tsv (default). tsv format gives back a
  data.frame object. xml gives back parsed xml as a list.

- sepfasta:

  (logical) If `TRUE`, the fasta data is separated into a list with
  names matching the processid's for each records. Works with both 'tsv'
  and 'xml' format. Note: This means multiple sequences can have the
  same name if a process id has multiple sequences. Default: `FALSE`

- cleanData:

  (logical) If `TRUE`, the cell values containing only duplicated values
  (ex : "COI-5P\|COI-5P\|COI-5P") will be reduce to one value ("COI-5P")
  and empty string will be change to NA. Default: `FALSE`

- ...:

  Further args passed on to
  [`crul::verb-GET`](https://docs.ropensci.org/crul/reference/verb-GET.html),
  main purpose being curl debugging

## Value

Either a data.frame, parsed xml, a http response object, or a list of
length two (data: a data.frame w/o nucleotide column, and fasta: a list
of nucleotides with the processid as name)

## Note

If using the `taxon` parameter with another parameter, if the `taxon`
isn't found in the public database, it will act as if no `taxon` was
specified and try to return all the data for the other specified
parameter. You can make sure that the `taxon` you're looking up has
public records with
[`bold_stats`](https://docs.ropensci.org/bold/reference/bold_stats.md).

## Large requests

Some requests can lead to errors. These often have to do with requesting
data for a rank that is quite high in the tree, such as an Order, for
example, Coleoptera. If your request is taking a long time, it's likely
that something will go wrong on the BOLD server side, or we'll not be
able to parse the result here in R because R can only process strings of
a certain length. `bold` users have reported errors in which the
resulting response from BOLD is so large that we could not parse it.

A good strategy for when you want data for a high rank is to do many
separate requests for lower ranks within your target rank. You can do
this manually, or use the function `taxize::downstream` to get all the
names of a lower rank within a target rank. There's an example in the
README (https://docs.ropensci.org/bold/#large-data)

## If a request times out

This is likely because you're request was for a large number of
sequences and the BOLD service timed out. You still should get some
output, those sequences that were retrieved before the time out
happened. As above, see the README
(https://docs.ropensci.org/bold/#large-data) for an example of dealing
with large data problems with this function.

## Marker

Notes from BOLD on the `marker` param: "All markers for a specimen
matching the search string will be returned. ie. A record with COI-5P
and ITS will return sequence data for both markers even if only COI-5P
was specified."

You will likely end up with data with markers that you did not request -
just be sure to filter those out as needed.

## References

http://v4.boldsystems.org/index.php/resources/api?type=webservices

## Examples

``` r
if (FALSE) { # \dontrun{
bold_seqspec(taxon='Osmia')
bold_seqspec(taxon='Osmia', format='xml')
bold_seqspec(taxon='Osmia', response=TRUE)
res <- bold_seqspec(taxon='Osmia', sepfasta=TRUE)
res$fasta[1:2]
res$fasta['GBAH0293-06']

# records that match a marker name
res <- bold_seqspec(taxon="Melanogrammus aeglefinus", marker="COI-5P")

# records that match a geographic locality
res <- bold_seqspec(taxon="Melanogrammus aeglefinus", geo="Canada")

## curl debugging
### You can do many things, including get verbose output on the curl call,
### and set a timeout
head(bold_seqspec(taxon='Osmia', verbose = TRUE))
head(bold_seqspec(taxon='Osmia', timeout_ms = 1))
} # }
```
