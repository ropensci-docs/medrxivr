# Provide information on the medRxiv snapshot used to perform the search

Provide information on the medRxiv snapshot used to perform the search

## Usage

``` r
mx_info(commit = "main", manifest_url = default_snapshot_manifest_url())
```

## Arguments

- commit:

  Deprecated. Only the default value "main" is supported. Use
  \`manifest_url\` to read a specific snapshot manifest.

- manifest_url:

  URL for a JSON snapshot manifest. Defaults to option
  \`medrxivr.snapshot_manifest\`, or the package's snapshot release
  manifest if that option is unset.

## Value

Message with snapshot details
