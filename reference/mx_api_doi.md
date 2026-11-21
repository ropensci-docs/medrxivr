# Access data on a single medRxiv/bioRxiv record via the Cold Spring Harbour Laboratory API

Provides programmatic access to data on a single preprint identified by
a unique Digital Object Identifier (DOI).

## Usage

``` r
mx_api_doi(doi, server = "medrxiv", clean = TRUE)
```

## Arguments

- doi:

  Digital object identifier of the preprint you wish to retrieve data
  on.

- server:

  Specify the server you wish to use: "medrxiv" (default) or "biorxiv"

- clean:

  Logical, defaulting to TRUE, indicating whether to clean the data
  returned by the API. If TRUE, variables containing absolute paths to
  the preprints web-page ("link_page") and PDF ("link_pdf") are
  generated from the "server", "DOI", and "version" variables returned
  by the API. The The "category", "authors" and "author_corresponding"
  variables are converted to title case. Finally, the "type" and
  "server" variables are dropped.

## Value

Dataframe containing details on the preprint identified by the DOI.

## See also

Other data-source:
[`mx_api_content()`](https://docs.ropensci.org/medrxivr/reference/mx_api_content.md),
[`mx_snapshot()`](https://docs.ropensci.org/medrxivr/reference/mx_snapshot.md)

## Examples

``` r
if (interactive()) {
  mx_data <- mx_api_doi("10.1101/2020.02.25.20021568")
}
```
