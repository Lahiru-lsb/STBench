# Plot UMAP comparisons across normalisation methods

Visualise previously calculated UMAP embeddings using one or multiple
colData annotations without recalculating PCA or UMAP.

## Usage

``` r
plot_umap_comparison(
  umap_data,
  colour_by = "region",
  point_size = 0.58,
  alpha = 0.6,
  ncol = 3,
  theme_name = "classic"
)
```

## Arguments

- umap_data:

  Data frame returned by get_umap_data().

- colour_by:

  Character vector containing one or more annotation columns.

- point_size:

  Point size for UMAP plots.

- alpha:

  Point transparency.

- ncol:

  Number of columns for single-annotation facets.

- theme_name:

  Plot theme.

## Value

A list containing plotting data and ggplot.

## Details

A single annotation uses facet_wrap by method. Multiple annotations use
facet_grid with methods in rows and annotations in columns.

## Examples

``` r
data(norm_example)

umap_data <- get_umap_data(
  norm_example,
  methods = NULL,
  prop_spots = 1,
  seed = 123,
  assay_name = "logcounts",
  n_pcs = 30,
  n_neighbors = 15
)
#> Running PCA and UMAP: None
#> Running PCA and UMAP: SpaNorm

p_umap_layer <- plot_umap_comparison(
  umap_data,
  colour_by = "cell_type",
  point_size = 0.58,
  alpha = 0.6,
  ncol = 3,
  theme_name = "classic"
)

p_umap_layer$plot
```
