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

## Examples

``` r
data(svg_example)

genes <- head(rownames(svg_example[[1]]), 5)

svg_df <- extract_svg_gene_set(
  svg_norm = svg_example,
  genes = genes,
  stat = "LR_stat",
  gene_id = "rownames",
  method_order = names(svg_example)
)

head(svg_df)
#>      gene   svg_stat  method
#> 1   HSPB7  0.4511002    None
#> 2   KCNC3 47.1932871    None
#> 3 COL25A1 10.2645509    None
#> 4     MAL 92.0936790    None
#> 5   CPXM2 -0.3092557    None
#> 6   HSPB7  0.4578449 SpaNorm
```
