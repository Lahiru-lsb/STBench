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
