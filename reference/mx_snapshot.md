# Access a static snapshot of the medRxiv repository

\[Available for medRxiv only\] This function allows users to import a
maintained static snapshot of the medRxiv repository, instead of
downloading a copy from the API, which can become unavailable during
peak usage times. The function reads a manifest-driven snapshot artifact
from the package's GitHub release assets by default.

## Usage

``` r
mx_snapshot(
  commit = "main",
  from_date = NULL,
  to_date = NULL,
  manifest_url = default_snapshot_manifest_url(),
  cache = TRUE
)
```

## Arguments

- commit:

  Deprecated. Only the default value "main" is supported. Use
  \`manifest_url\` to read a specific snapshot manifest.

- from_date:

  Optional earliest date of interest ("YYYY-MM-DD" or Date). If
  supplied, records with \`date\` earlier than this are excluded.

- to_date:

  Optional latest date of interest ("YYYY-MM-DD" or Date). If supplied,
  records with \`date\` later than this are excluded.

- manifest_url:

  URL for a JSON snapshot manifest. Defaults to option
  \`medrxivr.snapshot_manifest\`, or the package's latest GitHub release
  manifest if that option is unset.

- cache:

  Logical. If TRUE, downloaded manifest snapshot files are cached
  between sessions. Defaults to TRUE.

## Value

A formatted dataframe containing the data from the snapshot artifact,
with reconstructed \`link_page\` and \`link_pdf\` columns.

## See also

Other data-source:
[`mx_api_content()`](https://docs.ropensci.org/medrxivr/reference/mx_api_content.md),
[`mx_api_doi()`](https://docs.ropensci.org/medrxivr/reference/mx_api_doi.md)
