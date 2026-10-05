# Plot spatial expression across normalisation methods

Plot spatial expression of selected genes across multiple normalisation
methods.

## Usage

``` r
plot_spatial_expression(
  norm_list,
  genes,
  assay_name = "logcounts",
  method_order = NULL,
  scale_expr = TRUE,
  point_size = 0.5,
  colour_option = "magma",
  ncol_genes = 1,
  theme_name = "classic"
)
```

## Arguments

- norm_list:

  Named list of normalised SpatialExperiment objects.

- genes:

  Character vector containing genes to plot.

- assay_name:

  Name of assay containing expression values. Default is
  \`"logcounts"\`.

- method_order:

  Optional character vector specifying the order of normalisation
  methods.

- scale_expr:

  Logical. If TRUE, expression is scaled between 0 and 1 within each
  gene across all methods.

- point_size:

  Point size for spatial locations.

- colour_option:

  Viridis colour option.

- ncol_genes:

  Number of columns used when combining gene-specific unscaled plots.

- theme_name:

  Plot theme. One of \`"classic"\`, \`"bw"\`, \`"minimal"\`, or
  \`"gray"\`.

## Value

A list containing the plotting data and plot.

## Details

When \`scale_expr = TRUE\`, expression is scaled from 0 to 1 separately
for each gene across all normalisation methods. The resulting maps are
displayed using a facet grid with methods in rows and genes in columns.

When \`scale_expr = FALSE\`, the original expression values from the
selected assay are retained. A separate plot is created for each gene,
with normalisation methods shown as facets. Therefore, each gene has its
own colour scale.
