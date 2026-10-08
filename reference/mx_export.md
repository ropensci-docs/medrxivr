# Export references for preprints returning by a search to a .bib file

Export references for preprints returning by a search to a .bib file

## Usage

``` r
mx_export(data, file = "medrxiv_export.bib")
```

## Arguments

- data:

  Dataframe returned by mx_search() or mx_api\_\*() functions

- file:

  File location to save to. Must have the .bib file extension

## Value

Exports a formatted .BIB file, for import into a reference manager

## See also

Other helper:
[`mx_caps()`](https://docs.ropensci.org/medrxivr/reference/mx_caps.md),
[`mx_crosscheck()`](https://docs.ropensci.org/medrxivr/reference/mx_crosscheck.md),
[`mx_download()`](https://docs.ropensci.org/medrxivr/reference/mx_download.md)

## Examples

``` r
if (interactive()) {
  mx_results <- mx_search(mx_snapshot(), query = "brain")
  mx_export(mx_results, tempfile(fileext = ".bib"))
}
```
