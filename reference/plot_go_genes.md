# Plot cluster-specific DE genes used for GO

Plot the top cluster-specific DE genes detected under each normalisation
method.

## Usage

``` r
plot_go_genes(
  go_result,
  top_n = 5,
  method_col = "method",
  cluster_col = "cluster",
  gene_col = "gene",
  method_order = NULL,
  point_size = 3,
  palette = NULL,
  theme_name = "classic"
)
```

## Arguments

- go_result:

  Result returned by \`calculate_go()\`, or the gene data frame
  contained in \`go_result\$genes\`.

- top_n:

  Number of top DE genes shown per normalisation method and cluster.

- method_col:

  Name of the column containing normalisation methods.

- cluster_col:

  Name of the column containing clusters.

- gene_col:

  Name of the column containing gene names.

- method_order:

  Optional character vector specifying the order of normalisation
  methods.

- point_size:

  Point size.

- palette:

  Optional named character vector specifying colours for normalisation
  methods.

- theme_name:

  Plot theme. One of \`"classic"\`, \`"bw"\`, \`"minimal"\`, or
  \`"gray"\`.

## Value

A list containing plotting data and plot.
