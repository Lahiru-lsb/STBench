# Plot SVG statistic distribution for a gene set

Plot SVG statistic distribution for a gene set

## Usage

``` r
plot_svg_gene_set_distribution(
  svg_norm,
  genes,
  stat = "LR_stat",
  method_order = NULL,
  method_colors = NULL,
  gene_id = "rownames",
  transform = c("log1p", "log", "none"),
  plot_type = c("boxplot", "violin"),
  add_jitter = TRUE,
  point_size = 1.5,
  alpha = 0.6,
  theme_name = "classic"
)
```

## Arguments

- svg_norm:

  Named SVG results.

- genes:

  Gene set.

- stat:

  SVG statistic.

- method_order:

  Optional method order.

- method_colors:

  Optional named colours.

- gene_id:

  Gene identifier.

- transform:

  Transformation.

- plot_type:

  boxplot or violin.

- add_jitter:

  Add gene-level points.

- point_size:

  Point size.

- alpha:

  Point transparency.

- theme_name:

  Plot theme.

## Value

List containing data and plot.

## Examples

``` r
data(svg_example)

genes <- head(rownames(svg_example[[1]]), 10)

p <- plot_svg_gene_set_distribution(
  svg_norm = svg_example,
  genes = genes,
  stat = "LR_stat",
  transform = "log",
  plot_type = "boxplot"
)

p$plot
```
