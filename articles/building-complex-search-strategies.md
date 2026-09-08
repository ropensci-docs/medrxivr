# Building complex search strategies

## Building your search with Boolean operators

First load the `medrxivr` package:

``` r

library(medrxivr)
```

To find records that contain any of many terms, pass the terms as a
vector to the
[`mx_search()`](https://docs.ropensci.org/medrxivr/reference/mx_search.md)
function, as in the code chunk below. Query terms can include regular
expression syntax - see the [section at the end of this
document](#regex) on common regular expression that may be useful when
searching.

``` r

myquery <- c("dementia","vascular","alzheimer's") # Combined with Boolean OR

mx_results <- mx_search(data = mx_snapshot(),     # Use static snapshot for data
                        query = myquery)
#> Snapshot includes records through 2026-09-06
#> Found 9842 record(s) matching your search.
```

To find records relevant to more than one topic domain, create a vector
for each topic (note: there is no upper limit on the number of topics
your can have) and combine these vectors into a list which is then
passed to the
[`mx_search()`](https://docs.ropensci.org/medrxivr/reference/mx_search.md)
function:

``` r

topic1  <- c("dementia","vascular","alzheimer's")  # Combined with Boolean OR
topic2  <- c("lipids","statins","cholesterol")     # Combined with Boolean OR
myquery <- list(topic1, topic2)                    # Combined with Boolean AND

mx_results <- mx_search(data = mx_snapshot(),
                        query = myquery)
#> Snapshot includes records through 2026-09-06
#> Found 620 record(s) matching your search.
```

## Additional filters and options

### Limit search by field

By default, a range of fields (title, abstract, authors, category, and
DOI) are searched, but you can limit the search to a subset of these
using the `fields` argument:

``` r


# Limit search to title/abstract
mx_results <- mx_search(data = mx_snapshot(),
                        query = "dementia",
                        fields = c("title","abstract"))
#> Snapshot includes records through 2026-09-06
#> Found 1893 record(s) matching your search.

# Search by DOI
mx_results <- mx_search(data = mx_snapshot(),
                        query = "10.1101/2020.01.30.20019836",
                        fields = "doi")
#> Snapshot includes records through 2026-09-06
#> Found 1 record(s) matching your search.
```

### Exclude records containing certain terms

Often it is useful to be able to exclude records that contain a certain
term that is not relevant to your search. For example, in the search
below, we are looking for records related to “dementia” alone by
excluding those that mention “mild cognitive impairment”:

``` r

mx_results <- mx_search(data = mx_snapshot(),
                        query = "dementia",
                        NOT = "[Mm]ild cognitive impairment")
#> Snapshot includes records through 2026-09-06
#> Found 1596 record(s) matching your search.
```

### Limit by date posted

You can define either/both of the earliest and latest date you wish to
include records from. Note: the search is inclusive of both dates
specified:

``` r

mx_results <- mx_search(data = mx_snapshot(),
                        query = "dementia",
                        from_date = "2020-01-01",      # 1st Jan 2020
                        to_date = "2020-01-08")        # 8th Jan 2020
#> Snapshot includes records through 2026-09-06
#> Found 2 record(s) matching your search.
```

### Return multiple versions of a record

*medRxiv* allows authors to upload a new version of their preprint as
often as they like. By default, `medrxivr` only returns the most recent
version of the preprint, but if you are interested in exploring how a
record changed over time, you can retrieve all versions of the preprint
by setting `deduplicate = FALSE`

``` r

mx_results <- mx_search(data = mx_snapshot(),
                        query = "10.1101/2020.01.30.20019836",
                        fields = "doi",
                        deduplicate = FALSE)
#> Snapshot includes records through 2026-09-06
#> Found 4 record(s) matching your search.
#> Note, there may be >1 version of the same record.
```

## Useful syntax for the systematic reviewer

### Capitalisation

**Example regex:** `[Dd]ementia`  
**Description:** The search is case sensitive, so this syntax allows you
to find both **D**ementia and **d**ementia using a single term, rather
than having to enter them separately. However, setting the `autocaps`
argument of
[`mx_search()`](https://docs.ropensci.org/medrxivr/reference/mx_search.md)
to `TRUE` will automatically search for both capitalised and
uncapitalised versions of your search terms (e.g. with
`auto_caps = TRUE` you just need to search for “dementia” to find both
**D**ementia and **d**ementia - behind the scenes, “dementia” is
converted to “\[Dd\]ementia”.

### Wildcard

**Example regex:** `randomi*ation`  
**Description:** The wildcard operator “\*” defines any single
alphanumeric character - in this case, the term will find both
randomi**s**ation and randomi**z**ation.

### NEAR

**Example regex:** `systematic NEAR4 review`  
**Description:** The “NEAR4” operator defines that up to 4 words can be
between **systematic** and **review** and the search will still find it.
To change how far apart the terms are allowed to be, simply change the
number following NEAR (e.g. to find terms that are only one word apart,
the syntax would be `systematic NEAR1 review`). **Please note that the
search is directional, in that the example term here will find
“systematic methods for the review”, but will not find “the review was
systematic”.**

### Word limits

**Example regex:** `\\bNCOV\\b`  
**Description:** Sometimes it is useful to be able to define the start
and end of terms. For example, if you were searching for NCOV-19, simply
using `ncov` as your search term would also return records containing
u**ncov**ered. Using `\\b` allows you to define where the term beings
and ends, thus excluding false positive matches.

### Example using these regexes

To find records that contain “Mendelian” within 4 words of
“randomisation” (with varying capitalisation of “Mendelian” and UK/US
spellings of “randomisation”), the following syntax is correct:

``` r

mx_results <- mx_search(data = mx_snapshot(),
                        query = "mendelian NEAR4 randomi*ation", 
                        auto_caps = TRUE)
#> Snapshot includes records through 2026-09-06
#> Found 1432 record(s) matching your search.
```

### Regex tester

To check whether your search term will find what you expect it to, there
is a useful [regex
tester](https://spannbaueradam.shinyapps.io/r_regex_tester/), designed
by [Adam
Spannbauer](https://adamspannbauer.github.io/2018/01/16/r-regex-tester-shiny-app/).
