# Plot SVG statistic for selected genes

Plot SVG statistic for selected genes

## Usage

``` r
plot_svg_stat(
  svg_norm,
  genes,
  stat = "LR_stat",
  method_order = NULL,
  method_colors = NULL,
  transform = c("log1p", "log", "none"),
  point_size = 3,
  gene_id = "rownames",
  theme_name = "classic"
)
```

## Arguments

- svg_norm:

  Named list of SVG results.

- genes:

  Genes to plot.

- stat:

  SVG statistic.

- method_order:

  Optional method order.

- method_colors:

  Optional named vector of method colours.

- transform:

  Transformation: log1p, log, or none.

- point_size:

  Point size.

- gene_id:

  Gene identifier.

- theme_name:

  Plot theme.

## Value

A list containing data and plot.
