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

## Examples

``` r
# Create a small SpatialExperiment object
counts <- matrix(
  1:12,
  nrow = 3,
  dimnames = list(
    c("GeneA", "GeneB", "GeneC"),
    paste0("Cell", seq_len(4))
  )
)

spe <- SpatialExperiment::SpatialExperiment(
  assays = list(counts = counts)
)

SummarizedExperiment::rowData(spe)$LR_stat <- c(
  2.5, 4.0, 1.2
)

# Compare SVG statistics across normalization methods
svg_norm <- list(
  None = spe,
  scran = spe
)

result <- extract_svg_stats(
  svg_norm = svg_norm,
  genes = c("GeneA", "GeneB")
)

print(result)
#>    gene svg_stat method
#> 1 GeneA      2.5   None
#> 2 GeneB      4.0   None
#> 3 GeneA      2.5  scran
#> 4 GeneB      4.0  scran
```
