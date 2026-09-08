# Interacting with the Cold Spring Harbour Laboratory API

## Background

The [Cold Spring Harbour Laboratory API](https://api.biorxiv.org/)
provides a direct interface to the medRxiv and bioRxiv databases.
**However, the API does not allow you to perform searches,** instead
providing two endpoints that return either all content between two
specified dates or all information held on a particular DOI.

`medrxivr` provides two convenience functions for importing the data
provided by these endpoints in R:
[`mx_api_content()`](https://docs.ropensci.org/medrxivr/reference/mx_api_content.md)
and
[`mx_api_doi()`](https://docs.ropensci.org/medrxivr/reference/mx_api_doi.md).
The results of either function can then be passed to
[`mx_search()`](https://docs.ropensci.org/medrxivr/reference/mx_search.md)
for searching.

### By date range (`mx_api_content()`)

The format of this endpoint is
<https://api.biorxiv.org/details/%5Bserver%5D/%5Binterval%5D/%5Bcursor%5D>
where ‘interval’ must be two YYYY-MM-DD dates separated by ‘/’. Where
metadata for multiple papers is returned, results are paginated with 100
papers served in a call. The ‘cursor’ value can be used to iterate
through the result.

[`mx_api_content()`](https://docs.ropensci.org/medrxivr/reference/mx_api_content.md)
automatically moves through the pages for you, capturing all records
returned by the endpoint and returning them as an R object. For
instance,
<https://api.biorxiv.org/details/medrxiv/2020-01-01/2020-01-31/0> will
output 100 results (if that many remain) within the date range of
2020-01-01 to 2020-01-31 beginning from result 1. To import this into R
as a dataframe:

``` r

medrxiv_data <- mx_api_content(from_date = "2020-01-01", 
                               to_date = "2020-01-05")
#> Estimated total number of records as per API metadata: 33
#> Number of records retrieved from API: 33


biorxiv_data <- mx_api_content(server = "biorxiv",
                               from_date = "2020-01-01", 
                               to_date = "2020-01-05")
#> Estimated total number of records as per API metadata: 286
#> Number of records retrieved from API: 286
```

### By DOI (`mx_api_doi()`)

<https://api.biorxiv.org/details/%5Bserver%5D/%5BDOI%5D> returns detail
for a single manuscript. For instance,
<https://api.biorxiv.org/details/medrxiv/10.1101/2020.02.25.20021568>
will output metadata for the medRxiv paper with DOI
10.1101/2020.02.25.20021568. To import the results from this endpoint
into R as a dataframe:

``` r

mx_api_doi(doi = "10.1101/2020.02.25.20021568")
#> # A tibble: 2 × 16
#>   title  authors author_corresponding author_corresponding…¹ doi   date  version
#>   <chr>  <chr>   <chr>                <chr>                  <chr> <chr> <chr>  
#> 1 Deep … Chen, … Honggang Yu          Renmin Hospital of Wu… 10.1… 2020… 1      
#> 2 Deep … Chen, … Honggang Yu          Renmin Hospital of Wu… 10.1… 2020… 2      
#> # ℹ abbreviated name: ¹​author_corresponding_institution
#> # ℹ 9 more variables: license <chr>, category <chr>, jatsxml <chr>,
#> #   abstract <chr>, funder <lgl>, published <chr>, node <int>, link_page <chr>,
#> #   link_pdf <chr>
```

## Accessing the raw API data

Both functions contain a `clean` argument with is set to `TRUE` by
default. This is to ensure that the datasets returned by the
`mx_api_*()` functions can immediately be passed to
[`mx_search()`](https://docs.ropensci.org/medrxivr/reference/mx_search.md).
However, there may be occasions where this is not required, and so
setting this argument to `FALSE` will return the raw data provided by
the API endpoints. For example:

``` r

mx_api_content(to_date = "2019-07-01", clean = FALSE)
#> Estimated total number of records as per API metadata: 32
#> Number of records retrieved from API: 32
#> # A tibble: 32 × 15
#>    title authors author_corresponding author_corresponding…¹ doi   date  version
#>    <chr> <chr>   <chr>                <chr>                  <chr> <chr> <chr>  
#>  1 Mole… Daniel… Robert Castelo       "Department of Experi… 10.1… 2019… 1      
#>  2 Croh… Orna G… Orna G Ehrlich       "Crohn\\'s & Colitis … 10.1… 2019… 1      
#>  3 Upda… Joshua… Joshua D Wallach     "Yale School of Publi… 10.1… 2019… 1      
#>  4 Pred… Oliver… Olivera Stojanovic   "Institute of Cogniti… 10.1… 2019… 1      
#>  5 Pros… Nathan… Nathan Brajer        "Duke University Scho… 10.1… 2019… 1      
#>  6 Tren… Brian … Ben Goldacre         "University of Oxford" 10.1… 2019… 1      
#>  7 18F-… Nicola… Nicolas Nicastro     "University of Cambri… 10.1… 2019… 1      
#>  8 Perc… Sistan… Lena H Ting          "Emory University"     10.1… 2019… 1      
#>  9 Prox… Tesfa … Tesfa Dejenie Habte… "Department of Epidem… 10.1… 2019… 1      
#> 10 Tran… Alexan… Alexandre Vivot      "APHP"                 10.1… 2019… 1      
#> # ℹ 22 more rows
#> # ℹ abbreviated name: ¹​author_corresponding_institution
#> # ℹ 8 more variables: type <chr>, license <chr>, category <chr>, jatsxml <chr>,
#> #   abstract <chr>, funder <lgl>, published <chr>, server <chr>
```
