# Add quality-control metrics

Calculate basic spot-level and gene-level quality-control metrics from
raw counts in a SpatialExperiment object.

## Usage

``` r
add_qcs(spe, assay_name = "counts", mito_pattern = "^MT-")
```

## Arguments

- spe:

  A SpatialExperiment object.

- assay_name:

  Name of assay containing raw counts. Default is \`"counts"\`.

- mito_pattern:

  Regular expression used to identify mitochondrial genes from row
  names. Default is \`"^MT-"\`.

## Value

A SpatialExperiment object with QC metrics added to \`colData()\` and
\`rowData()\`.

## Details

Spot-level metrics include library size, log library size, number of
detected genes, and mitochondrial proportion.

Gene-level metrics include mean expression and log mean expression.

## Examples

``` r
data(spe_example)

spe_qc <- add_qcs(
  spe_example,
  assay_name = "counts",
  mito_pattern = "^MT-"
)
#> Loading required namespace: SpatialExperiment
#> Warning: No mitochondrial genes matched '^MT-'.
#' @import sparseMatrixStats
```
