# Search for terms in the dataset

Search for terms in the dataset

## Usage

``` r
run_search(mx_data, query, fields, deduplicate, NOT = "")
```

## Arguments

- mx_data:

  The mx_dataset filtered for the date limits

- query:

  Character string, vector or list

- fields:

  Fields of the database to search - default is Title, Abstract,
  Authors, Category, and DOI.

- deduplicate:

  Logical. Only return the most recent version of a record. Default is
  TRUE.

- NOT:

  Vector of regular expressions to exclude from the search. Default is
  NULL.

## See also

Other main:
[`mx_reporter()`](https://docs.ropensci.org/medrxivr/reference/mx_reporter.md),
[`mx_search()`](https://docs.ropensci.org/medrxivr/reference/mx_search.md),
[`print_full_results()`](https://docs.ropensci.org/medrxivr/reference/print_full_results.md)
