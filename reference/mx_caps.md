# Search term wrapper that allows for different capitalization of term

Inspired by the varying capitalization of "NCOV" during the corona virus
pandemic (e.g. ncov, nCoV, NCOV, nCOV), this function allows for all
possible configurations of lower- and upper-case letters in your search
term.

## Usage

``` r
mx_caps(x)
```

## Arguments

- x:

  Search term to be formatted

## Value

The input string is return, but with each non-space character repeated
in lower- and upper-case, and enclosed in square brackets. For example,
mx_caps("ncov") returns "\[Nn\]\[Cc\]\[Oo\]\[Vv\]"

## See also

Other helper:
[`mx_crosscheck()`](https://docs.ropensci.org/medrxivr/reference/mx_crosscheck.md),
[`mx_download()`](https://docs.ropensci.org/medrxivr/reference/mx_download.md),
[`mx_export()`](https://docs.ropensci.org/medrxivr/reference/mx_export.md)
