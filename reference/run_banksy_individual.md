# Run BANKSY clustering independently for each slice

Run BANKSY clustering independently across normalisation methods and
spatial slices.

## Usage

``` r
run_banksy_individual(
  norm_list,
  methods = names(norm_list),
  assay_name = "logcounts",
  cluster_col = "banksy_cluster",
  k_geom = 15,
  lambda = 0.8,
  resolution = 0.2,
  seed = 123
)
```

## Arguments

- norm_list:

  Named list containing normalised SpatialExperiment objects.

- methods:

  Optional character vector specifying the normalisation methods to
  analyse.

- assay_name:

  Name of the assay used by BANKSY.

- cluster_col:

  Name of the colData column used to store BANKSY cluster assignments.

- k_geom:

  Number of spatial neighbours used by BANKSY.

- lambda:

  BANKSY spatial weighting parameter.

- resolution:

  Resolution parameter used for clustering.

- seed:

  Random seed for reproducibility.

## Value

Named list with the same structure as \`norm_list\`. BANKSY cluster
assignments are added to the colData of each SpatialExperiment object.

## Details

BANKSY cluster assignments are added to the colData of each
SpatialExperiment object so that the same objects can be used in
downstream clustering evaluation, plotting, differential expression, and
GO enrichment analyses.

The function supports either:

- a named list of SpatialExperiment objects, or

- a named list where each method contains a named list of
  SpatialExperiment objects corresponding to multiple slices.
