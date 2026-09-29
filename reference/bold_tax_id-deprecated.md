# Search BOLD for taxonomy data by BOLD ID.

Search BOLD for taxonomy data by BOLD ID.

## Arguments

- id:

  (integer) One or more BOLD taxonomic identifiers. required.

- dataTypes:

  (character) Specifies the datatypes that will be returned. 'all'
  returns all data. 'basic' returns basic taxon information. 'images'
  returns specimen images.

- includeTree:

  (logical) If `TRUE` (default: `FALSE`), returns a list containing
  information for parent taxa as well as the specified taxon.

- response:

  (logical) Default : FALSE. If TRUE, returns the object from the Curl
  call. Useful for debugging and getting more detailed info on the API
  call.

- ...:

  Further args passed on to
  [`crul::verb-GET`](https://docs.ropensci.org/crul/reference/verb-GET.html),
  main purpose being curl debugging

## See also

[`bold-deprecated`](https://docs.ropensci.org/bold/reference/bold-deprecated.md)
