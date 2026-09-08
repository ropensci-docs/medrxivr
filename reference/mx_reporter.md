# Search and print output for individual search items

Search and print output for individual search items

## Usage

``` r
mx_reporter(mx_data, num_results, query, fields, deduplicate, NOT)
```

## Arguments

- mx_data:

  The mx_dataset filtered for the date limits

- num_results:

  The number of results returned by the overall search

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
  "".

## See also

Other main:
[`mx_search()`](https://docs.ropensci.org/medrxivr/reference/mx_search.md),
[`print_full_results()`](https://docs.ropensci.org/medrxivr/reference/print_full_results.md),
[`run_search()`](https://docs.ropensci.org/medrxivr/reference/run_search.md)
