# Access medRxiv/bioRxiv data via the Cold Spring Harbour Laboratory API

Provides programmatic access to all preprints available through the Cold
Spring Harbour Laboratory API, which serves both the medRxiv and bioRxiv
preprint repositories.

## Usage

``` r
mx_api_content(
  from_date = "2013-01-01",
  to_date = as.character(Sys.Date()),
  clean = TRUE,
  server = "medrxiv",
  include_info = FALSE
)
```

## Arguments

- from_date:

  Earliest date of interest, written as "YYYY-MM-DD". Defaults to 1st
  Jan 2013 ("2013-01-01"), ~6 months prior to earliest preprint
  registration date.

- to_date:

  Latest date of interest, written as "YYYY-MM-DD". Defaults to current
  date.

- clean:

  Logical, defaulting to TRUE, indicating whether to clean the data
  returned by the API. If TRUE, variables containing absolute paths to
  the preprints web-page ("link_page") and PDF ("link_pdf") are
  generated from the "server", "DOI", and "version" variables returned
  by the API. The The "category", "authors" and "author_corresponding"
  variables are converted to title case. Finally, the "type" and
  "server" variables are dropped.

- server:

  Specify the server you wish to use: "medrxiv" (default) or "biorxiv"

- include_info:

  Logical, indicating whether to include variables containing
  information returned by the API (e.g. API status, cursor number, total
  count of papers, etc). Default is FALSE.

## Value

Dataframe with 1 record per row

## See also

Other data-source:
[`mx_api_doi()`](https://docs.ropensci.org/medrxivr/reference/mx_api_doi.md),
[`mx_snapshot()`](https://docs.ropensci.org/medrxivr/reference/mx_snapshot.md)

## Examples

``` r
if (interactive()) {
  mx_data <- mx_api_content(
    from_date = "2020-01-01",
    to_date = "2020-01-07"
  )
}
```
