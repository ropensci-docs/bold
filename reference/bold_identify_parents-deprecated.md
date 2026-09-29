# Add taxonomic parent names to a data.frame

Add taxonomic parent names to a data.frame

## Arguments

- x:

  (data.frame/list) list of data.frames - the output from a call to
  [`bold_identify`](https://docs.ropensci.org/bold/reference/bold_identify.md).
  or a single data.frame from the output from same. required.

- wide:

  (logical) output in long or wide format. See Details. Default: `FALSE`

- taxid:

  (character) A taxid name. Optional. See `Filtering` below.

- taxon:

  (character) A taxon name. Optional. See `Filtering` below.

- tax_rank:

  (character) A tax_rank name. Optional. See `Filtering` below.

- tax_division:

  (character) A tax_division name. Optional. See `Filtering` below.

- parentid:

  (character) A parentid name. Optional. See `Filtering` below.

- parentname:

  (character) A parentname name. Optional. See `Filtering` below.

- taxonrep:

  (character) A taxonrep name. Optional. See `Filtering` below.

- specimenrecords:

  (character) A specimenrecords name. Optional. See `Filtering` below.

- ...:

  Further args passed on to
  [`verb-GET`](https://docs.ropensci.org/crul/reference/verb-GET.html),
  main purpose being curl debugging

## See also

[`bold-deprecated`](https://docs.ropensci.org/bold/reference/bold-deprecated.md)
