# Separate sequences (fasta) from `bold_seqspec` output.

Separate sequences (fasta) from `bold_seqspec` output.

## Usage

``` r
b_sepFasta(x, format = "tsv")
```

## Arguments

- x:

  (object) The output of a `bold_seqspec` call.

- format:

  (character) The format used in the `bold_seqspec` call. One of 'tsv'
  (default) or 'xml'.

## Value

A list of length two : the specimen data and the sequences list.

## Examples

``` r
if (FALSE) { # \dontrun{
res <- bold_seqspec(taxon='Osmia')
res <- b_sepFasta(res)
# (same as bold_seqspec(taxon='Osmia', sepFasta = TRUE))
} # }
```
