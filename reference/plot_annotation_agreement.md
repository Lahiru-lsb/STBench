# Plot pairwise cell-type annotation agreement

Plot pairwise annotation agreement between normalisation methods as a
heatmap.

## Usage

``` r
plot_annotation_agreement(
  norm_list,
  annotation_col = "SingleR_label",
  method_order = NULL,
  remove_na = TRUE,
  show_values = TRUE,
  digits = 2,
  colour_option = "viridis",
  theme_name = "classic"
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

  Logical. If TRUE, missing annotations are removed before agreement is
  calculated.

- show_values:

  Logical. If TRUE, agreement values are displayed inside heatmap cells.

- digits:

  Number of decimal places shown in heatmap cells.

- colour_option:

  Viridis colour option.

- theme_name:

  Plot theme. One of \`"classic"\`, \`"bw"\`, \`"minimal"\`, or
  \`"gray"\`.

## Value

A list containing agreement data and plot.
