# Check how up-to-date the maintained medRxiv snapshot is

Provides information on how up-to-date the maintained medRxiv snapshot
provided by \`mx_snapshot()\` is by checking whether there have been any
records added to, or updated in, the medRxiv repository since the last
snapshot was taken.

## Usage

``` r
mx_crosscheck()
```

## See also

Other helper:
[`mx_caps()`](https://docs.ropensci.org/medrxivr/reference/mx_caps.md),
[`mx_download()`](https://docs.ropensci.org/medrxivr/reference/mx_download.md),
[`mx_export()`](https://docs.ropensci.org/medrxivr/reference/mx_export.md)

## Examples

``` r
if (interactive()) {
  mx_crosscheck()
}
```
