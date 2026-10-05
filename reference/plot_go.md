# Plot GO enrichment results

Plot the top enriched Gene Ontology terms for each cluster across
normalisation methods.

## Usage

``` r
plot_go(
  go_result,
  top_n = 5,
  method_col = "method",
  cluster_col = "cluster",
  method_order = NULL,
  point_size_range = c(2, 7),
  theme_name = "classic"
)
```

## Arguments

- go_result:

  Result returned by \`calculate_go()\`, or the GO data frame contained
  in \`go_result\$go\`.

- top_n:

  Number of top GO terms shown per normalisation method and cluster.

- method_col:

  Name of the column containing normalisation methods.

- cluster_col:

  Name of the column containing clusters.

- method_order:

  Optional character vector specifying the order of normalisation
  methods.

- point_size_range:

  Numeric vector defining minimum and maximum point size.

- theme_name:

  Plot theme. One of \`"classic"\`, \`"bw"\`, \`"minimal"\`, or
  \`"gray"\`.

## Value

A list containing plotting data and plot.

## Details

Point size represents gene count, colour represents enrichment
significance, and shape represents normalisation method.
