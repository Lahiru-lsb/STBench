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
#>                                          61 
#>             Choroid plexus epithelial cells 
#>                                          58 
#>               Dentate gyrus granule neurons 
#>                                          47 
#>    Di- and mesencephalon excitatory neurons 
#>                                          82 
#>    Di- and mesencephalon inhibitory neurons 
#>                                          14 
#>                             Ependymal cells 
#>                                          17 
#>                                   Microglia 
#>                                          32 
#>               Non-glutamatergic neuroblasts 
#>                                          24 
#>                            Oligodendrocytes 
#>                                         121 
#>                         Peptidergic neurons 
#>                                          74 
#>                                   Pericytes 
#>                                          16 
#>       Telencephalon inhibitory interneurons 
#>                                          31 
#> Telencephalon projecting excitatory neurons 
#>                                          59 
#> Telencephalon projecting inhibitory neurons 
#>                                          48 
#>                                 Unannotated 
#>                                          56 
#>           Vascular and leptomeningeal cells 
#>                                          48 
#>                  Vascular endothelial cells 
#>                                          43 
#>                Vascular smooth muscle cells 
#>                                          13 
```
