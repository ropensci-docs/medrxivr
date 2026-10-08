# Search preprint data

Search preprint data

## Usage

``` r
mx_search(
  data = NULL,
  query = NULL,
  fields = c("title", "abstract", "authors", "category", "doi"),
  from_date = NULL,
  to_date = NULL,
  auto_caps = FALSE,
  NOT = "",
  deduplicate = TRUE,
  report = FALSE
)
```

## Arguments

- data:

  The preprint dataset that is to be searched, created either using
  mx_api_content() or mx_snapshot()

- query:

  Character string, vector or list

- fields:

  Fields of the database to search - default is Title, Abstract,
  Authors, Category, and DOI.

- from_date:

  Defines earliest date of interest. Written in the format "YYYY-MM-DD".
  Note, records published on the date specified will also be returned.

- to_date:

  Defines latest date of interest. Written in the format "YYYY-MM-DD".
  Note, records published on the date specified will also be returned.

- auto_caps:

  As the search is case sensitive, this logical specifies whether the
  search should automatically allow for differing capitalisation of
  search terms. For example, when TRUE, a search for "dementia" would
  find both "dementia" but also "Dementia". Note, that if your term is
  multi-word (e.g. "systematic review"), only the first word is
  automatically capitalised (e.g your search will find both "systematic
  review" and "Systematic review" but won't find "Systematic Review".
  Note that this option will format terms in the query and NOT arguments
  (if applicable).

- NOT:

  Vector of regular expressions to exclude from the search. Default is
  "".

- deduplicate:

  Logical. Only return the most recent version of a record. Default is
  TRUE.

- report:

  Logical. Run mx_reporter. Default is FALSE.

## See also

Other main:
[`mx_reporter()`](https://docs.ropensci.org/medrxivr/reference/mx_reporter.md),
[`print_full_results()`](https://docs.ropensci.org/medrxivr/reference/print_full_results.md),
[`run_search()`](https://docs.ropensci.org/medrxivr/reference/run_search.md)

## Examples

``` r
if (interactive()) {
  # Using the static snapshot
  mx_results <- mx_search(data = mx_snapshot(), query = "dementia")
}
```
