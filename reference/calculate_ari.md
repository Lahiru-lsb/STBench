# Calculate adjusted Rand index

Calculate the adjusted Rand index between clustering assignments and
user-specified ground-truth labels across normalisation methods and
spatial slices.

## Usage

``` r
calculate_ari(
  norm_list,
  ground_truth_col,
  cluster_col = "banksy_cluster",
  methods = names(norm_list)
)
```

## Arguments

- norm_list:

  Named list of SpatialExperiment objects containing clustering results.

- ground_truth_col:

  Name of the colData column containing ground-truth labels.

- cluster_col:

  Name of the colData column containing cluster assignments.

- methods:

  Optional character vector specifying the normalisation methods to
  analyse.

## Value

A data frame containing ARI values for each normalisation method and
spatial slice.
