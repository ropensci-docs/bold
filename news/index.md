# Changelog

## bold 1.3.0

CRAN release: 2023-05-02

#### NEW FEATURES

- New function
  [`bold_identify_taxonomy()`](https://docs.ropensci.org/bold/reference/bold_identify_taxonomy.md)
  to add taxonomic information to the output of
  [`bold_identify()`](https://docs.ropensci.org/bold/reference/bold_identify.md)
  and replace
  [`bold_identify_parents()`](https://docs.ropensci.org/bold/reference/bold-deprecated.md).
  Instead of taking the taxon names from the
  [`bold_identify()`](https://docs.ropensci.org/bold/reference/bold_identify.md)
  output, and use
  [`bold_tax_name()`](https://docs.ropensci.org/bold/reference/bold_tax_name.md)
  to get the taxonomic ID to then pass it to
  [`bold_tax_id()`](https://docs.ropensci.org/bold/reference/bold-deprecated.md)
  to get the parent names, we take the process ids from the
  [`bold_identify()`](https://docs.ropensci.org/bold/reference/bold_identify.md)
  output and then pass them to
  [`bold_specimens()`](https://docs.ropensci.org/bold/reference/bold_specimens.md).
  This has the advantages of being faster and, more importantly, making
  sure the correct taxonomy is returned. The function has less arguments
  since the filtering of the result isn’t necessary anymore. Since the
  result now has only one line per row of input, the output is always in
  ‘wide’ format (like when using
  [`bold_identify_parents()`](https://docs.ropensci.org/bold/reference/bold-deprecated.md)
  with `wide=TRUE`). There is one new argument `taxOnly` which is `TRUE`
  by default and return only the taxonomic data. However, since
  [`bold_specimens()`](https://docs.ropensci.org/bold/reference/bold_specimens.md)
  also returns other data (habitat, country, image_url, etc), setting
  this argument to `FALSE` will also join that data to the input.

- New function
  [`bold_tax_id2()`](https://docs.ropensci.org/bold/reference/bold_tax_id2.md)
  which will eventually replace
  [`bold_tax_id()`](https://docs.ropensci.org/bold/reference/bold-deprecated.md).
  The main changes are in the format of the output. For the `dataTypes`
  ‘basic’, ‘stats’, ‘images’ and ‘thirdparty’, the output doesn’t
  change. For the `dataTypes` ‘sequencinglabs’, ‘geo’ and ‘depository’,
  instead of having one (sometimes very) wide data.frame, the result is
  now in ‘long’ format, with the columns ‘input’, ‘taxid’,
  ‘sequencinglabs\|country\|depository’ and ‘count’. For the `dataTypes`
  ‘all’ or when selecting more than one dataTypes, the output is a list
  for each data types containing their respective data.frame. When
  setting includeTree to `TRUE`, the parents’ data is rbinded to their
  respective data.frame. The function also check that all arguments are
  the correct type and that the `dataTypes` chosen are valid.

- The now deprecated
  [`bold_tax_id()`](https://docs.ropensci.org/bold/reference/bold-deprecated.md)
  has the same argument checks as
  [`bold_tax_id2()`](https://docs.ropensci.org/bold/reference/bold_tax_id2.md)
  but will throw warnings instead of errors to not affect existing
  workflows. Also, if a chosen `dataTypes` is invalid, it gets removed
  to not make unnecessary requests.

- Similarly, the now deprecated
  [`bold_identify_parents()`](https://docs.ropensci.org/bold/reference/bold-deprecated.md)
  has new argument checks and will throw warnings to not affect existing
  workflows.

- For
  [`bold_tax_id2()`](https://docs.ropensci.org/bold/reference/bold_tax_id2.md)
  and
  [`bold_tax_name()`](https://docs.ropensci.org/bold/reference/bold_tax_name.md),
  when querying multiple taxa, if one fails, the loop won’t break and
  will instead throw the API error as a warning. The output object will
  also have 2 new attributes “errors” and “params” that will let you see
  what errors occurred for with request and what parameters were use for
  the request. To make it easy to retrieve these attributes, 3 new
  functions have been created:

  - [`bold_get_attr()`](https://docs.ropensci.org/bold/reference/bold_get_attr.md)
    will return a list of the two attributes
  - [`bold_get_errors()`](https://docs.ropensci.org/bold/reference/bold_get_attr.md)
    will return a list of the errors
  - [`bold_get_params()`](https://docs.ropensci.org/bold/reference/bold_get_attr.md)
    will return a list of parameters used

- [`bold_specimens()`](https://docs.ropensci.org/bold/reference/bold_specimens.md)
  and
  [`bold_seqspec()`](https://docs.ropensci.org/bold/reference/bold_seqspec.md)
  have a new parameter `cleanData` which, when set to `TRUE`, replaces
  empty strings (““) by NAs and strings containing only duplicated
  values by their unique value (ex :”COI-5P\|COI-5P\|COI-5P” becomes
  “COI-5P”).

- New function
  [`bold_read_trace()`](https://docs.ropensci.org/bold/reference/bold_trace.md)
  to replace
  [`read_trace()`](https://docs.ropensci.org/bold/reference/bold_trace.md).
  Can read one or multiple trace files from a `boldtrace` object or
  provided file path(s).

- New function
  [`b_sepFasta()`](https://docs.ropensci.org/bold/reference/b_sepFasta.md)
  to use after a call to
  [`bold_seqspec()`](https://docs.ropensci.org/bold/reference/bold_seqspec.md)
  where `sepFasta` wasn’t set to `TRUE`.

#### MINOR IMPROVEMENTS

- made tests for the new functions
- made tests for the
  [`bold_trace()`](https://docs.ropensci.org/bold/reference/bold_trace.md)
  function
- added test to existing functions to improved test coverage
- added/completed argument checks for every functions
- [`bold_specimens()`](https://docs.ropensci.org/bold/reference/bold_specimens.md)
  and
  [`bold_seqspec()`](https://docs.ropensci.org/bold/reference/bold_seqspec.md)
  can now also return partial output like
  [`bold_seq()`](https://docs.ropensci.org/bold/reference/bold_seq.md)
- using `data.table` when possible, removed `dplyr` and `reshape`
  dependencies
- using `stringi` instead of `stringr` which removed `stringr`’s other
  dependencies
- added more details to the documentation of some functions

#### BUG FIXES

- changed how http responses are read so they throw warnings and return
  NAs instead of errors. This prevents a long request to stop and fail,
  loosing the already fetched data.
  ([\#74](https://github.com/ropensci/bold/issues/74))
- added a note in the documentation of
  [`bold_seq()`](https://docs.ropensci.org/bold/reference/bold_seq.md),
  [`bold_seqspec()`](https://docs.ropensci.org/bold/reference/bold_seqspec.md)
  and `bold_specimen()` that if the `taxon` doesn’t have public records,
  if using another parameter will return all data for that parameter.
  Users can verify the availability of public records with
  [`bold_stats()`](https://docs.ropensci.org/bold/reference/bold_stats.md).
  A note was also added in
  [`bold_tax_name()`](https://docs.ropensci.org/bold/reference/bold_tax_name.md)
  that the column ‘specimenrecords’ relate to the records in the
  taxonomy browser and not in the public data portal.
  ([\#76](https://github.com/ropensci/bold/issues/76))
- fixed output of bold_seq()
  ([\#79](https://github.com/ropensci/bold/issues/79))
- changed the function used to encode to UTF-8
  ([\#81](https://github.com/ropensci/bold/issues/81),
  [\#86](https://github.com/ropensci/bold/issues/86))
- contacted bold so they would fix their typo in ‘depository’ which
  prevented fetching related data with
  [`bold_tax_id()`](https://docs.ropensci.org/bold/reference/bold-deprecated.md)
  ([\#83](https://github.com/ropensci/bold/issues/83)). Added a line in
  the function to change ‘depositories’ to ‘depository’ in case people
  had been using that.
- added a check for ‘name’ in
  [`bold_tax_name()`](https://docs.ropensci.org/bold/reference/bold_tax_name.md)
  to double escape single quotes. Otherwise it doesn’t return the data
  ([\#84](https://github.com/ropensci/bold/issues/84),
  [\#85](https://github.com/ropensci/bold/issues/85)). Since it’s
  related to the API, this means that the data that comes back also
  contains errors. So I added a function to repair the names of ‘taxon’,
  ‘taxonrep’ and ‘parentname’ in the returned object. The function is
  also used in `pipe_params()` (which is used by
  [`bold_seq()`](https://docs.ropensci.org/bold/reference/bold_seq.md),
  [`bold_seqspec()`](https://docs.ropensci.org/bold/reference/bold_seqspec.md)
  and `bold_specimen()`) to repair the `taxon` parameter in case users
  use results from previous versions.
- changed the way the response of
  [`bold_seqspec()`](https://docs.ropensci.org/bold/reference/bold_seqspec.md)
  is read ([\#87](https://github.com/ropensci/bold/issues/87),
  [\#88](https://github.com/ropensci/bold/issues/88)) thanks
  [@cjfields](https://github.com/cjfields)
- added a note in
  [`bold_stats()`](https://docs.ropensci.org/bold/reference/bold_stats.md)
  documentation to specify that the record counts include all gene
  markers ([\#90](https://github.com/ropensci/bold/issues/90)).

## bold 1.2.0

CRAN release: 2021-05-11

#### MINOR IMPROVEMENTS

- vignettes fix ([\#77](https://github.com/ropensci/bold/issues/77))

## bold 1.1.0

CRAN release: 2020-06-17

#### MINOR IMPROVEMENTS

- fix a failing test
  ([\#73](https://github.com/ropensci/bold/issues/73))

## bold 1.0.0

CRAN release: 2020-05-01

#### MINOR IMPROVEMENTS

- change base url for all requests to https from http
  ([\#70](https://github.com/ropensci/bold/issues/70))
- fixed a warning arising from use of
  [`bold_seqspec()`](https://docs.ropensci.org/bold/reference/bold_seqspec.md) -
  we now set the encoding to “UTF-8” before parsing the string to XML
  ([\#71](https://github.com/ropensci/bold/issues/71))
- [`bold_seqspec()`](https://docs.ropensci.org/bold/reference/bold_seqspec.md)
  fix: capture “Fatal errors” returned by BOLD servers and pass that
  along to the user with advice
  ([\#66](https://github.com/ropensci/bold/issues/66))
- add “Marker” and “Large requests” documentation sections to both
  [`bold_seq()`](https://docs.ropensci.org/bold/reference/bold_seq.md)
  and
  [`bold_seqspec()`](https://docs.ropensci.org/bold/reference/bold_seqspec.md).
  the marker section details that the marker parameter doesn’t actually
  filter results that you get - but you can filter them yourself. the
  large requests section gives some caveats associated with large data
  requests and outlines how to sort it out
  ([\#61](https://github.com/ropensci/bold/issues/61))

## bold 0.9.0

CRAN release: 2019-06-27

#### MINOR IMPROVEMENTS

- improved test coverage
  ([\#58](https://github.com/ropensci/bold/issues/58))
- allow curl options to be passed into
  [`bold_identify_parents()`](https://docs.ropensci.org/bold/reference/bold-deprecated.md)
  ([\#64](https://github.com/ropensci/bold/issues/64))
- fix instructions in README for package `sangerseqR` - instructions
  depend on which version of R is being used
  ([\#65](https://github.com/ropensci/bold/issues/65)) thanks
  [@KevCaz](https://github.com/KevCaz)

#### BUG FIXES

- fixes in package for `_R_CHECK_LENGTH_1_LOGIC2_`
  ([\#57](https://github.com/ropensci/bold/issues/57))
- [`bold_identify()`](https://docs.ropensci.org/bold/reference/bold_identify.md)
  fix: ampersands needed to be escaped
  ([\#62](https://github.com/ropensci/bold/issues/62)) thanks
  [@devonorourke](https://github.com/devonorourke)

## bold 0.8.6

CRAN release: 2018-12-14

#### MINOR IMPROVEMENTS

- tests that make HTTP requests now use package `vcr` to cache
  responses, speeds up tests significantly, and no longer relies on an
  internet connection
  ([\#55](https://github.com/ropensci/bold/issues/55))
  ([\#56](https://github.com/ropensci/bold/issues/56))
- [`bold_seq()`](https://docs.ropensci.org/bold/reference/bold_seq.md):
  sometimes on large requests, the BOLD servers time out, and give back
  partial output but don’t indicate that there was an error. We catch
  this kind of error now, throw a message for the user, and the function
  gives back the partial output given by the server. Also added to the
  documentation for
  [`bold_seq()`](https://docs.ropensci.org/bold/reference/bold_seq.md)
  and in the README that if you run into this problem try to do many
  queries that will result in smaller set of results instead of one or
  fewer larger queries
  ([\#52](https://github.com/ropensci/bold/issues/52))
  ([\#53](https://github.com/ropensci/bold/issues/53))
- [`bold_seq()`](https://docs.ropensci.org/bold/reference/bold_seq.md):
  remove return characters (`\r` and `\n`) from sequences
  ([\#54](https://github.com/ropensci/bold/issues/54))

## bold 0.8.0

CRAN release: 2018-10-26

#### MINOR IMPROVEMENTS

- link to taxize bookdown book in readme and vignette
  ([\#51](https://github.com/ropensci/bold/issues/51))
- [`bold_identify_parents()`](https://docs.ropensci.org/bold/reference/bold-deprecated.md)
  gains many new parameters (`taxid`, `taxon`, `tax_rank`,
  `tax_division`, `parentid`, `parentname`, `taxonrep`,
  `specimenrecords`) to filter parents based on any of a number of
  fields - should solve problem where multiple parents found for a
  single taxon, often in different kingdoms
  ([\#50](https://github.com/ropensci/bold/issues/50))
- add note in docs of
  [`bold_identify()`](https://docs.ropensci.org/bold/reference/bold_identify.md)
  that the function uses `lapply` internally, so queries with lots of
  sequences can take a long time

#### BUG FIXES

- fix
  [`bold_specimens()`](https://docs.ropensci.org/bold/reference/bold_specimens.md):
  use [`rawToChar()`](https://rdrr.io/r/base/rawConversion.html) on raw
  bytes instead of [`parse()`](https://rdrr.io/r/base/parse.html) from
  `crul` ([\#47](https://github.com/ropensci/bold/issues/47))

## bold 0.5.0

CRAN release: 2017-07-21

#### NEW FEATURES

- Now using BOLD’s v4 API throughout the package. This was essentially
  just a change of the BASE URL for each request
  ([\#30](https://github.com/ropensci/bold/issues/30))
- Now using `crul` for HTTP requests. Only really affects users in that
  specifying curl options works slightly differenlty
  ([\#42](https://github.com/ropensci/bold/issues/42))

#### BUG FIXES

- `marker` parameter in `bold_seqspec` was and maybe still is not
  working, in the sense that using the parameter doesn’t always limit
  results to the marker you specify. Not really fixed - watch out for
  it, and filter after you get results back to get markers you want.
  ([\#25](https://github.com/ropensci/bold/issues/25))
- Fixed bug in `bold_identify_parents` - was failing when no match for a
  parent name. ([\#41](https://github.com/ropensci/bold/issues/41)) thx
  [@VascoElbrecht](https://github.com/VascoElbrecht)
- `tsv` results were erroring in `bold_specimens` and other fxns
  ([\#46](https://github.com/ropensci/bold/issues/46)) - fixed by
  switching to new BOLD v4 API
  ([\#30](https://github.com/ropensci/bold/issues/30))

#### MINOR IMPROVEMENTS

- Namespace calls to base pkgs for `stats` and `utils` - replaced `is`
  with `inherits` ([\#39](https://github.com/ropensci/bold/issues/39))

## bold 0.4.0

CRAN release: 2017-01-06

#### NEW FEATURES

- New function
  [`bold_identify_parents()`](https://docs.ropensci.org/bold/reference/bold-deprecated.md)
  to add taxonomic information to the output of
  [`bold_identify()`](https://docs.ropensci.org/bold/reference/bold_identify.md).
  We take the taxon names from `bold_identify` output, and use
  `bold_tax_name` to get the taxonomic ID, passing it to `bold_tax_id`
  to get the parent names, then attaches those to the input data. There
  are two options given what you put for the `wide` parameter. If `TRUE`
  you get data.frames of the same dimensions with parent rank name and
  ID as new columns (for each name going up the hierarchy) - while if
  `FALSE` you get a long data.frame. thanks
  [@dougwyu](https://github.com/dougwyu) for inspiring this
  ([\#36](https://github.com/ropensci/bold/issues/36))

#### MINOR IMPROVEMENTS

- replace
  [`xml2::xml_find_one`](http://xml2.r-lib.org/reference/xml_find_all.md)
  with
  [`xml2::xml_find_first`](http://xml2.r-lib.org/reference/xml_find_all.md)
  ([\#33](https://github.com/ropensci/bold/issues/33))
- Fix description of `db` options in `bold_identify` man file - COX1 and
  COX1_SPECIES were switched
  ([\#37](https://github.com/ropensci/bold/issues/37)) thanks for
  pointing that out [@dougwyu](https://github.com/dougwyu)

#### BUG FIXES

- Fix to `bold_tax_id` for when some elements returned from the BOLD API
  were empty/`NULL` ([\#32](https://github.com/ropensci/bold/issues/32))
  thanks [@fmichonneau](https://github.com/fmichonneau) !!

## bold 0.3.5

CRAN release: 2016-03-29

#### MINOR IMPROVEMENTS

- Added more tests to the test suite
  ([\#28](https://github.com/ropensci/bold/issues/28))

#### BUG FIXES

- Fixed a bug in an internal data parser
  ([\#27](https://github.com/ropensci/bold/issues/27))

## bold 0.3.4

CRAN release: 2016-03-23

#### NEW FEATURES

- Added a code of conduct

#### MINOR IMPROVEMENTS

- Switched to `xml2` from `XML` as the XML parser for this package
  ([\#26](https://github.com/ropensci/bold/issues/26))
- Fixes to
  [`bold_trace()`](https://docs.ropensci.org/bold/reference/bold_trace.md)
  to create dir and tar file when it doesn’t already exist

#### BUG FIXES

- Fixed odd problem where sometimes resulting data from HTTP request was
  garbled on `content(x, "text")`, so now using `rawToChar(content(x))`,
  which works ([\#24](https://github.com/ropensci/bold/issues/24))

## bold 0.3.0

CRAN release: 2015-09-16

#### MINOR IMPROVEMENTS

- Explicitly import non-base R functions
  ([\#22](https://github.com/ropensci/bold/issues/22))
- Better package level manual file

## bold 0.2.6

CRAN release: 2015-04-18

#### MINOR IMPROVEMENTS

- `sangerseqR` package now in Suggests for reading trace files, and is
  only used in
  [`bold_trace()`](https://docs.ropensci.org/bold/reference/bold_trace.md)
  function.
- General code tidying, reduction of code duplication.
- [`bold_trace()`](https://docs.ropensci.org/bold/reference/bold_trace.md)
  gains two new parameters: `overwrite` to choose whether to overwrite
  an existing file of the same name or not, `progress` to show a
  progress bar for downloading or not.
- [`bold_trace()`](https://docs.ropensci.org/bold/reference/bold_trace.md)
  gains a print method to show a tidy summary of the trace file
  downloaded.

#### BUG FIXES

- Fixed similar bugs in
  [`bold_tax_name()`](https://docs.ropensci.org/bold/reference/bold_tax_name.md)
  ([\#17](https://github.com/ropensci/bold/issues/17)) and
  [`bold_tax_id()`](https://docs.ropensci.org/bold/reference/bold-deprecated.md)
  ([\#18](https://github.com/ropensci/bold/issues/18)) in which species
  that were missing from the BOLD database returned empty arrays but 200
  status codes. Parsing those as failed attempts now. Also fixes problem
  in taxize in `bold_search()` that use these two functions.

## bold 0.2.0

CRAN release: 2014-08-20

#### NEW FEATURES

- Package gains two new functions for working with the BOLD taxonomy
  APIs:
  [`bold_tax_name()`](https://docs.ropensci.org/bold/reference/bold_tax_name.md)
  and
  [`bold_tax_id()`](https://docs.ropensci.org/bold/reference/bold-deprecated.md),
  which search for taxonomic data from BOLD using either names or BOLD
  identifiers, respectively.
  ([\#11](https://github.com/ropensci/bold/issues/11))
- Two new packages in Imports: `jsonlite` and `reshape`.

#### MINOR IMPROVEMENTS

- Added new taxonomy API functions to the vignette
  ([\#14](https://github.com/ropensci/bold/issues/14))
- Added reference URLS to all function doc files to allow easy reference
  for the appropriate API docs.
- `callopts` parameter changed to `...` throughout the package, so that
  passing on options to `httr::GET` is done via named parameters, e.g.,
  `config=verbose()`.
  ([\#13](https://github.com/ropensci/bold/issues/13))
- Added examples of doing curl debugging throughout man pages.

## bold 0.1.2

CRAN release: 2014-07-24

#### MINOR IMPROVEMENTS

- Improved the vignette
  ([\#8](https://github.com/ropensci/bold/issues/8))
- Added small function to print helpful message when user inputs no
  parameters or zero length parameter values.

#### BUG FIXES

- Fixed some broken tests with the new `httr` (v0.4)
  ([\#9](https://github.com/ropensci/bold/issues/9)), and added a few
  more tests ([\#7](https://github.com/ropensci/bold/issues/7))

## bold 0.1.0

CRAN release: 2014-05-29

#### NEW FEATURES

- released to CRAN
