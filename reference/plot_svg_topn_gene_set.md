# Proportion of a gene set among top-ranked SVGs

Proportion of a gene set among top-ranked SVGs

## Usage

``` r
plot_svg_topn_gene_set(
  svg_norm,
  genes,
  top_n = c(50, 100, 200, 300),
  method_order = NULL,
  method_colors = NULL,
  gene_id = "rownames",
  theme_name = "classic"
)
```

## Arguments

- svg_norm:

  Named SVG results.

- genes:

  Gene set, such as housekeeping genes.

- top_n:

  Vector containing top-N values.

- method_order:

  Optional method order.

- method_colors:

  Optional named colours.

- gene_id:

  Gene identifier.

- theme_name:

  Plot theme.

## Value

List containing data and plot.
