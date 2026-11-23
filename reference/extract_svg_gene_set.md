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
#>    gene   svg_stat  method
#> 1 Ptgds  57.347071    None
#> 2   MBP 457.322353    None
#> 3  PLTP  18.833916    None
#> 4   Vtn   8.300816    None
#> 5  Penk 150.665360    None
#> 6 Ptgds  80.428930 SpaNorm
```
