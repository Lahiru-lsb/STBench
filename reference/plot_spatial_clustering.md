# Plot spatial clustering results

Plot spatial cluster assignments stored in the colData of
SpatialExperiment objects across normalisation methods.

## Usage

``` r
plot_spatial_clustering(
  norm_list,
  cluster_col = "banksy_cluster",
  methods = names(norm_list),
  method_order = NULL,
  point_size = 0.5,
  palette = NULL,
  ncol = 3,
  legend_point_size = 4,
  theme_name = "classic"
)
```

## Arguments

- norm_list:

  Named list of SpatialExperiment objects containing clustering results.

- cluster_col:

  Name of the colData column containing cluster assignments.

- methods:

  Optional character vector specifying the normalisation methods to
  plot.

- method_order:

  Optional character vector specifying the order of normalisation
  methods.

- point_size:

  Point size for spatial locations.

- palette:

  Optional named character vector specifying colours for clusters.

- ncol:

  Number of facet columns when only one slice is present.

- legend_point_size:

  Point size used in the legend.

- theme_name:

  Plot theme. One of \`"classic"\`, \`"bw"\`, \`"minimal"\`, or
  \`"gray"\`.

## Value

A list containing plotting data, palette, and plot.

## Details

By default, cluster colours are generated using the Polychrome 36-colour
palette.
