# Plot SVG ranks for selected genes

Plot SVG ranks for selected genes

## Usage

``` r
plot_svg_rank(
  svg_norm,
  genes,
  method_order = NULL,
  method_colors = NULL,
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

- method_order:

  Optional method order.

- method_colors:

  Optional method colours.

- point_size:

  Point size.

- gene_id:

  Gene identifier.

- theme_name:

  Plot theme.

## Value

List containing data and plot.

## Examples

``` r
data(svg_example)

marker_genes <- head(rownames(svg_example[[1]]), 5)

p <- plot_svg_rank(
  svg_norm = svg_example,
  genes = marker_genes
)

p$plot
```
