# Calculate pairwise cell-type annotation agreement

Calculate the proportion of spatial locations receiving the same
cell-type annotation between each pair of normalisation methods.

## Usage

``` r
calculate_annotation_agreement(
  norm_list,
  annotation_col = "SingleR_label",
  method_order = NULL,
  remove_na = TRUE
)
```

## Arguments

- norm_list:

  Named list of annotated SpatialExperiment objects.

- annotation_col:

  Name of the colData column containing cell-type annotations.

- method_order:

  Optional character vector specifying the order of normalisation
  methods.

- remove_na:

  Logical. If TRUE, spatial locations with a missing annotation in
  either method are removed before calculating agreement.

## Value

A data frame containing pairwise annotation agreement.
