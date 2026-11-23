# Run cell-type annotation

Run cell-type annotation for a named list of normalised
SpatialExperiment objects using SingleR.

## Usage

``` r
run_annotation(
  norm_list,
  ref,
  labels,
  method = "SingleR",
  label_name = "SingleR_label",
  pruned_label_name = "SingleR_pruned_label",
  ...
)
```

## Arguments

- norm_list:

  Named list of normalised SpatialExperiment objects.

- ref:

  Reference SingleCellExperiment or SummarizedExperiment object.

- labels:

  Character vector containing reference cell-type labels. Length must
  equal the number of columns in \`ref\`.

- method:

  Cell-type annotation method. Currently only \`"SingleR"\` is
  supported.

- label_name:

  Name of the colData column used to store predicted labels.

- pruned_label_name:

  Name of the colData column used to store pruned SingleR labels.

- ...:

  Additional parameters passed to \`SingleR::SingleR()\`.

## Value

Named list of annotated SpatialExperiment objects.

## Details

Predicted labels are added to the colData of each SpatialExperiment
object so that the same objects can be used in downstream plotting and
benchmarking functions.

## Examples

``` r
data(norm_example)

# Use a subset of cells as an illustrative reference
ref <- norm_example$None[, seq_len(100)]
labels <- as.character(ref$cell_type)

# Annotate the remaining cells
query <- lapply(
  norm_example,
  function(spe) spe[, seq.int(101, ncol(spe))]
)

annotated_norm <- run_annotation(
  norm_list = query,
  ref = ref,
  labels = labels,
  method = "SingleR",
  label_name = "SingleR_label",
  pruned_label_name = "SingleR_pruned_label",
  de.method = "classic"
)
#> Running SingleR: None
#> Detected a SingleCellExperiment as the reference dataset, consider setting
#> 'de.method = "t"' or "wilcox" in trainSingleR(). If you know better, this hint
#> can be disabled with 'hint.sce=FALSE'.
#> Running SingleR: SpaNorm
#> Detected a SingleCellExperiment as the reference dataset, consider setting
#> 'de.method = "t"' or "wilcox" in trainSingleR(). If you know better, this hint
#> can be disabled with 'hint.sce=FALSE'.

table(annotated_norm$None$SingleR_label)
#> 
#>                                  Astrocytes 
#>                                         105 
#>             Choroid plexus epithelial cells 
#>                                          19 
#>               Dentate gyrus granule neurons 
#>                                          23 
#>    Di- and mesencephalon excitatory neurons 
#>                                          58 
#>    Di- and mesencephalon inhibitory neurons 
#>                                          46 
#>                             Ependymal cells 
#>                                          16 
#>                                   Microglia 
#>                                          19 
#>               Non-glutamatergic neuroblasts 
#>                                          42 
#>                            Oligodendrocytes 
#>                                         137 
#>                         Peptidergic neurons 
#>                                          35 
#>                                   Pericytes 
#>                                          20 
#>       Telencephalon inhibitory interneurons 
#>                                          24 
#> Telencephalon projecting excitatory neurons 
#>                                         206 
#> Telencephalon projecting inhibitory neurons 
#>                                          54 
#>           Vascular and leptomeningeal cells 
#>                                          36 
#>                  Vascular endothelial cells 
#>                                          42 
#>                Vascular smooth muscle cells 
#>                                          18 
```
