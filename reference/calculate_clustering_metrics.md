# Calculate BANKSY clustering evaluation metrics

Calculates ARI, NMI, homogeneity, completeness, and spatial average
silhouette width (ASW) for each normalisation method and spatial slice.
Overall is the unweighted mean of NMI, HOM, and COM; it is a
user-defined composite agreement score rather than a standard accuracy
measure.

## Usage

``` r
calculate_clustering_metrics(
  norm_list,
  ground_truth_col,
  cluster_col = "banksy_cluster",
  methods = names(norm_list),
  nmi_variant = "sum",
  asw_max_cells = 3000L,
  seed = 123L
)
```

## Arguments

- norm_list:

  Named list of SpatialExperiment objects, or a named list whose
  elements are named lists of SpatialExperiment objects (slices).

- ground_truth_col:

  Name of the colData column containing reference labels.

- cluster_col:

  Name of the colData column containing predicted clusters.

- methods:

  Optional vector of normalisation methods to evaluate.

- nmi_variant:

  NMI normalisation; one of "sum", "max", "min", "sqrt", or "joint".
  "sum" uses arithmetic-mean entropy normalization.

- asw_max_cells:

  Maximum number of cells used to calculate spatial ASW per slice.
  Larger slices are randomly subsampled.

- seed:

  Integer random seed for reproducible ASW subsampling.

## Value

Data frame with method, slice, n, ARI, NMI, HOM, COM, ASW, Overall,
n_asw, and ASW_sampled.

## Details

ASW uses Euclidean distances between the first two spatial coordinates,
not expression-space distances. For large slices, ASW is estimated from
a random subset of cells to limit memory requirements.

## Examples

``` r
data(norm_example)

banksy_norm <- run_banksy_individual(
  norm_list = norm_example,
  seed = 123
)
#> Computing neighbors...
#> Spatial mode is kNN_median
#> Parameters: k_geom=15
#> Done
#> Done
#> Using seed=123
#> Using seed=123
#> Computing neighbors...
#> Spatial mode is kNN_median
#> Parameters: k_geom=15
#> Done
#> Done
#> Using seed=123
#> Using seed=123

metrics_df <- calculate_clustering_metrics(
  norm_list = banksy_norm,
  ground_truth_col = "layer_guess",
  cluster_col = "banksy_cluster"
)

metrics_df
#>    method  slice    n       ARI       NMI       HOM       COM          ASW
#> 1    None slice1 1000 0.3453591 0.4775199 0.3465493 0.7676278  0.075250048
#> 2 SpaNorm slice1 1000 0.2700809 0.4334076 0.3461446 0.5794992 -0.002975939
#>     Overall n_asw ASW_sampled
#> 1 0.5305656  1000       FALSE
#> 2 0.4530171  1000       FALSE
```
