# Download PDF's of preprints returned by a search

Download PDF's of all the papers in your search results

## Usage

``` r
mx_download(
  mx_results,
  directory,
  create = TRUE,
  name = c("ID", "DOI"),
  print_update = 10
)
```

## Arguments

- mx_results:

  Vector containing the links to the medRxiv PDFs

- directory:

  The location you want to download the PDF's to

- create:

  TRUE or FALSE. If TRUE, creates the directory if it doesn't exist

- name:

  How to name the downloaded PDF. By default, both the ID number of the
  record and the DOI are used.

- print_update:

  How frequently to print an update

## See also

Other helper:
[`mx_caps()`](https://docs.ropensci.org/medrxivr/reference/mx_caps.md),
[`mx_crosscheck()`](https://docs.ropensci.org/medrxivr/reference/mx_crosscheck.md),
[`mx_export()`](https://docs.ropensci.org/medrxivr/reference/mx_export.md)

## Examples

``` r
if (interactive()) {
  mx_results <- mx_search(mx_snapshot(), query = "10.1101/2020.02.25.20021568")
  mx_download(mx_results, directory = tempdir())
}
```
