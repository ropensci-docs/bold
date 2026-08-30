# Get BOLD trace files

Get BOLD trace files

## Usage

``` r
bold_trace(
  taxon = NULL,
  ids = NULL,
  bin = NULL,
  container = NULL,
  institutions = NULL,
  researchers = NULL,
  geo = NULL,
  marker = NULL,
  dest = NULL,
  overwrite = TRUE,
  progress = TRUE,
  ...
)

# S3 method for class 'boldtrace'
print(x, ...)

read_trace(x)

bold_read_trace(x)
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

  (character) Returns all records containing matching marker codes.

- dest:

  (character) A directory to write the files to

- overwrite:

  (logical) Overwrite existing directory and file?

- progress:

  (logical) Print progress or not. NOT AVAILABLE FOR NOW. HOPEFULLY WILL
  RETURN SOON.

- ...:

  Further args passed on to
  [`verb-GET`](https://docs.ropensci.org/crul/reference/verb-GET.html)

- x:

  (list or character) Either the boldtrace object returned from
  `bold_trace` or the path(s) of bold trace file(s).

## References

http://v4.boldsystems.org/index.php/resources/api?type=webservices

## Examples

``` r
if (FALSE) { # \dontrun{
# Use a specific destination directory
bold_trace(taxon = "Bombus ignitus", geo = "Japan", dest = "~/mytarfiles")

# Another example
# bold_trace(ids='ACRJP618-11', dest="~/mytarfiles")
# bold_trace(ids=c('ACRJP618-11','ACRJP619-11'), dest="~/mytarfiles")

# read file in
x <- bold_trace(ids=c('ACRJP618-11','ACRJP619-11'), dest="~/mytarfiles")
(res <- read_trace(x$ab1[2]))
# read all files in
(res <- read_trace(x))

# The progress dialog is pretty verbose, so quiet=TRUE is a nice touch,
# but not by default
# Beware, this one take a while
# x <- bold_trace(taxon='Osmia', quiet=TRUE)

if (requireNamespace("sangerseqR", quietly = TRUE)) {
 library("sangerseqR")
 primarySeq(res)
 secondarySeq(res)
 head(traceMatrix(res))
}
} # }
```
