# Allow for capitalisation of search terms

Allow for capitalisation of search terms

## Usage

``` r
fix_caps(x)
```

## Arguments

- x:

  Search query to be formatted. Note, any search term already containing
  a square bracket will not be reformatted to preserve user-defined
  regexes.

## Value

The same list or vector search terms, but with proper regular expression
syntax to allow for capitalisation of the first letter of each term.
