# Search for matches to sequences against the BOLD COI database.

Search for matches to sequences against the BOLD COI database.

## Usage

``` r
bold_identify(
  sequences,
  db = c("COX1", "COX1_SPECIES", "COX1_SPECIES_PUBLIC", "COX1_L640bp"),
  response = FALSE,
  keepSeq = TRUE,
  ...
)
```

## Arguments

- sequences:

  (character) A vector or list of sequences to identify. Required. See
  Details.

- db:

  (character) The database to match against, one of COX1 (default),
  COX1_SPECIES, COX1_SPECIES_PUBLIC, OR COX1_L640bp. See Details for
  more information.

- response:

  (logical) Note that response is the object that returns from the Curl
  call, useful for debugging, and getting detailed info on the API call.

- keepSeq:

  (logical) If TRUE (default), returns each data.frame with an attribute
  'sequence' containing sequence used to get those results.

- ...:

  Further args passed on to
  [`verb-GET`](https://docs.ropensci.org/crul/reference/verb-GET.html),
  main purpose being curl debugging

## Value

A data.frame or list of (one per sequences) with the top specimen
matches (up to 100) and their details. If the query fails, returns
`NULL`. Each data.frame has the attributes `sequence` with the provided
sequence to match (unless keepSeq is set to FALSE) and `errors` with the
error message given from a failed request.

## Details

BOLD only allows one sequences per query. We internally
[`lapply`](https://rdrr.io/r/base/lapply.html) over the input values
given to the sequences\` parameter to search with one sequences per
query. Remember this if you have a lot of sequences - you are doing a
separate query for each one, so it can take a long time - if you run
into errors let us know.

## db parameter options

- COX1 Every COI barcode record on BOLD with a minimum sequences length
  of 500bp (warning: unvalidated library and includes records without
  species level identification). This includes many species represented
  by only one or two specimens as well as all species with interim
  taxonomy. This search only returns a list of the nearest matches and
  does not provide a probability of placement to a taxon.

- COX1_SPECIES Every COI barcode record with a species level
  identification and a minimum sequences length of 500bp. This includes
  many species represented by only one or two specimens as well as all
  species with interim taxonomy. Note : Sometimes it does return matches
  that don't have a species level identification. Will be checking with
  BOLD.

- COX1_SPECIES_PUBLIC All published COI records from BOLD and GenBank
  with a minimum sequences length of 500bp. This library is a collection
  of records from the published projects section of BOLD.

- OR COX1_L640bp Subset of the Species library with a minimum sequences
  length of 640bp and containing both public and private records. This
  library is intended for short sequences identification as it provides
  maximum overlap with short reads from the barcode region of COI.

## Named outputs

For a named output list, make sure to pass in a named list or vector to
the `sequences` parameter. You can use `names<-` or
[`setNames`](https://rdrr.io/r/stats/setNames.html) to set names on a
list or vector of sequences.

## References

http://v4.boldsystems.org/index.php/resources/api?type=idengine

## See also

[`bold_identify_parents`](https://docs.ropensci.org/bold/reference/bold-deprecated.md)

## Examples

``` r
if (FALSE) { # \dontrun{
seq <- sequences$seq1
res <- bold_identify(sequences=seq)
head(res[[1]])
head(bold_identify(sequences=seq, db='COX1_SPECIES')[[1]])
} # }
```
