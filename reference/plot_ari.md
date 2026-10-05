# Plot adjusted Rand index

Create a dot plot of adjusted Rand index values across normalisation
methods.

## Usage

``` r
plot_ari(
  ari_df,
  method_col = "method",
  ari_col = "ARI",
  method_order = NULL,
  point_size = 4,
  palette = NULL,
  theme_name = "classic"
)
```

## Arguments

- ari_df:

  Data frame returned by \`calculate_ari()\`.

- method_col:

  Name of the column containing normalisation methods.

- ari_col:

  Name of the column containing ARI values.

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
