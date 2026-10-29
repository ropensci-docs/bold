# Add taxonomic parent names to a data set containing the process IDs of identified sequences.

Add taxonomic parent names to a data set containing the process IDs of
identified sequences.

## Usage

``` r
bold_identify_taxonomy(x, taxOnly = TRUE)

# S4 method for class 'list'
bold_identify_taxonomy(x, taxOnly = TRUE)

# S4 method for class 'matrix'
bold_identify_taxonomy(x, taxOnly = TRUE)

# S4 method for class 'data.frame'
bold_identify_taxonomy(x, taxOnly = TRUE)

# S4 method for class 'missing'
bold_identify_taxonomy(x, taxOnly = TRUE)
```

## Arguments

- x:

  A single data.frame or matrix, or a list of. Usually the output from a
  call to
  [`bold_identify`](https://docs.ropensci.org/bold/reference/bold_identify.md).
  Required.

- taxOnly:

  (logical) If TRUE (Default), only the taxonomic names and ids are
  added (equivalent format to the results of
  [`bold_identify_parents`](https://docs.ropensci.org/bold/reference/bold-deprecated.md)
  when `wide`is set to TRUE. If FALSE, also joins the rest of the data
  returned by
  [`bold_specimens`](https://docs.ropensci.org/bold/reference/bold_specimens.md).

## Value

a data.frame or a list of data.frames with added taxonomic
classification.

## Details

This function gets the process ids from the input data.frame(s) (ID
column), then queries
[`bold_specimens`](https://docs.ropensci.org/bold/reference/bold_specimens.md)
to get the sample information and adds it to the input data.frame(s).

Records in the input data that do not have matches for parent names
simply get NA values in the added columns.

## Examples

``` r
if (FALSE) { # \dontrun{
seqs <- bold_identify(sequences = bold::sequences$seq2)

seqs_tax <- bold_identify_taxonomy(seqs)
head(seqs_tax[[1]])

x <- bold_seq(taxon = "Satyrium")
seqs <- bold_identify(x$sequence[1:2])
seqs_tax <- bold_identify_taxonomy(seqs)
seqs_tax
} # }
```
