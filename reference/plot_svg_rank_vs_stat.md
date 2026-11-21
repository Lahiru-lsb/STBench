# Plot SVG Rank Against SVG Statistic

Visualises the relationship between SVG statistics and SVG ranks for
selected genes across normalisation methods.

## Usage

``` r
plot_svg_rank_vs_stat(
  svg_norm,
  genes,
  stat = "LR_stat",
  method_order = NULL,
  method_colors = NULL,
  transform = c("log1p", "log", "none"),
  scales = c("fixed", "free", "free_x", "free_y"),
  ncol = NULL,
  nrow = NULL,
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

  SVG statistic. Default is "LR_stat".

- method_order:

  Optional method order.

- method_colors:

  Optional named vector of method colours.

- transform:

  Transformation: log1p, log, or none.

- scales:

  Facet scales: fixed, free, free_x, or free_y.

- ncol:

  Number of facet columns.

- nrow:

  Number of facet rows.

- point_size:

  Point size.

- gene_id:

  Gene identifier.

- theme_name:

  Plot theme.

## Value

A list containing data and plot.

## Details

Each point represents a normalisation method, with genes displayed in
separate facets.

## Examples

``` r
data(svg_example)

marker_genes <- head(rownames(svg_example[[1]]), 5)

p <- plot_svg_rank_vs_stat(
  svg_norm = svg_example,
  genes = marker_genes,
  stat = "LR_stat",
  transform = "log"
)

p$plot
```
