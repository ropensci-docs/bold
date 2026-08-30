# bold

bold: A programmatic interface to the Barcode of Life data

## About

This package gives you access to data from BOLD System
http://www.boldsystems.org/ via their API
(http://v4.boldsystems.org/index.php/api_home)

## Functions

- [`bold_specimens`](https://docs.ropensci.org/bold/reference/bold_specimens.md) -
  Search for specimen data

- [`bold_seq`](https://docs.ropensci.org/bold/reference/bold_seq.md) -
  Search for and retrieve sequences

- [`bold_seqspec`](https://docs.ropensci.org/bold/reference/bold_seqspec.md) -
  Get sequence and specimen data together

- [`bold_trace`](https://docs.ropensci.org/bold/reference/bold_trace.md) -
  Get trace files - saves to disk

- [`read_trace`](https://docs.ropensci.org/bold/reference/bold_trace.md) -
  Read trace files into R

- [`bold_tax_name`](https://docs.ropensci.org/bold/reference/bold_tax_name.md) -
  Get taxonomic names via input names

- [`bold_tax_id`](https://docs.ropensci.org/bold/reference/bold-deprecated.md) -
  Get taxonomic names via BOLD identifiers (Deprecated)

- [`bold_tax_id2`](https://docs.ropensci.org/bold/reference/bold_tax_id2.md) -
  Get taxonomic names via BOLD identifiers (improved)

- [`bold_identify`](https://docs.ropensci.org/bold/reference/bold_identify.md) -
  Search for match given a COI sequence

- [`bold_identify_parents`](https://docs.ropensci.org/bold/reference/bold-deprecated.md) -
  Adds guessed parent ranks (Deprecated)

- [`bold_identify_taxonomy`](https://docs.ropensci.org/bold/reference/bold_identify_taxonomy.md) -
  Adds real parent ranks.

Interestingly, they provide xml and tsv format data for the specimen
data, while they provide fasta data format for the sequence data. So for
the specimen data you can get back raw XML, or a data frame parsed from
the tsv data, while for sequence data you get back a list (b/c sequences
are quite long and would make a data frame unwieldy).
