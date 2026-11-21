# Calculate UMAP embeddings across normalisation methods

Perform PCA and UMAP independently for each normalisation method using
the same sampled spots and common genes.

## Usage

``` r
get_umap_data(
  norm,
  methods = NULL,
  prop_spots = 1,
  seed = 123,
  assay_name = "logcounts",
  n_pcs = 30,
  n_neighbors = 15
)
```

## Arguments

- norm:

  Named list of normalised SpatialExperiment objects.

- methods:

  Character vector of methods to compare. If NULL, all available methods
  are used.

- prop_spots:

  Proportion of spots to sample.

- seed:

  Random seed.

- assay_name:

  Assay used for PCA and UMAP.

- n_pcs:

  Number of principal components.

- n_neighbors:

  Number of UMAP neighbours.

## Value

Data frame containing UMAP coordinates, method, spot identifiers, and
all colData annotations.

## Details

All colData annotations from the reference object are retained for
subsequent plotting.

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
#> Warning: You're computing too large a percentage of total singular values, use a standard svd instead.
#> Running PCA and UMAP: SpaNorm
#> Warning: You're computing too large a percentage of total singular values, use a standard svd instead.
```
