# Extract SVG statistics for a gene set

Extract SVG statistics for a gene set

## Usage

``` r
extract_svg_gene_set(
  svg_norm,
  genes,
  stat = "LR_stat",
  gene_id = "rownames",
  method_order = NULL
)
```

## Arguments

- svg_norm:

  Named SVG results.

- genes:

  Character vector containing genes.

- stat:

  SVG statistic.

- gene_id:

  Gene identifier.

- method_order:

  Optional method order.

## Value

Data frame.
