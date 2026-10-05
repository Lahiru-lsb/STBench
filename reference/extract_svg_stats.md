# Extract SVG statistics for selected genes

Extract SVG statistics for selected genes

## Usage

``` r
extract_svg_stats(
  svg_norm,
  genes,
  stat = "LR_stat",
  gene_id = "rownames",
  method_order = NULL
)
```

## Arguments

- svg_norm:

  Named list of SVG results.

- genes:

  Character vector of genes.

- stat:

  SVG statistic column.

- gene_id:

  Gene identifier.

- method_order:

  Optional method order.

## Value

Data frame.
