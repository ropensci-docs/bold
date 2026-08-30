# Get the error messages and parameters used for a request from a bold output.

Get the error messages and parameters used for a request from a bold
output.

Get the error messages from a bold output.

Get the parameters used for a request from a bold output.

## Usage

``` r
bold_get_attr(x)

bold_get_errors(x)

bold_get_params(x)
```

## Arguments

- x:

  Any object with an attribute "params". Usually the output of
  [`bold_tax_name`](https://docs.ropensci.org/bold/reference/bold_tax_name.md)
  or
  [`bold_tax_id2`](https://docs.ropensci.org/bold/reference/bold_tax_id2.md).

## Value

A list of the attributes 'errors' and 'params' of the object.

The 'errors' attribute of the object.

The 'params' attribute of the object.

## Examples

``` r
if (FALSE) { # \dontrun{
x <- bold_tax_name(name=c("Apis","Felis","Pinus"), tax_division = "Animalia")
bold_get_errors(x)
y <- bold_tax_id2(id = c(88899999, 125295, NA_integer_), dataTypes = c("basic", "stats"))
bold_get_errors(y)
} # }
if (FALSE) { # \dontrun{
x <- bold_tax_name(name=c("Apis","Felis","Pinus"), tax_division = "Animalia")
bold_get_errors(x)
y <- bold_tax_id2(id = c(88899999, 125295, NA_integer_), dataTypes = c("basic", "stats"))
bold_get_errors(y)
} # }
if (FALSE) { # \dontrun{
x <- bold_tax_name(name=c("Apis","Felis","Pinus"), tax_division = "Animalia")
bold_get_params(x)
y <- bold_tax_id2(id = c(88899999, 125295, NA_integer_), dataTypes = c("basic", "stats"))
bold_get_params(y)
} # }
```
