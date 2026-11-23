# Calculate clustering metrics across gene-selection strategies

Calculate ARI, NMI, HOM, COM, spatial ASW, and Overall clustering
agreement for each gene-selection strategy.

## Usage

``` r
calculate_gene_selection_metrics(
  banksy_list,
  ground_truth_col = "layer_guess",
  cluster_col = "banksy_cluster",
  asw_max_cells = 3000,
  seed = 123
)
```

## Arguments

- banksy_list:

  Output from run_banksy_gene_selection().

- ground_truth_col:

  Ground-truth annotation column.

- cluster_col:

  Predicted cluster column.

- asw_max_cells:

  Maximum cells used for spatial ASW.

- seed:

  Random seed.

## Value

Data frame containing clustering metrics and gene sets. \#' @examples
data(norm_example)

banksy_genes \<- run_banksy_gene_selection( norm_list = norm_example,
methods = names(norm_example), gene_selection = "all", assay_name =
"logcounts", k_geom = 15, lambda = 0.8, resolution = 0.2, seed = 123 )

metrics_genes \<- calculate_gene_selection_metrics( banksy_list =
banksy_genes, ground_truth_col = "layer_guess" )

## Examples

``` r
data(norm_example)

banksy_results <- run_banksy_individual(
  norm_list = norm_example,
  methods = names(norm_example),
  assay_name = "logcounts",
  cluster_col = "banksy_cluster",
  k_geom = 15,
  lambda = 0.8,
  resolution = 0.2,
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

banksy_list <- list(all = banksy_results)

metrics_genes <- calculate_gene_selection_metrics(
  banksy_list = banksy_list,
  ground_truth_col = "layer_guess",
  cluster_col = "banksy_cluster",
  asw_max_cells = 3000,
  seed = 123
)

head(metrics_genes)
#>    method  slice    n       ARI       NMI       HOM       COM          ASW
#> 1    None slice1 1000 0.3453591 0.4775199 0.3465493 0.7676278  0.075250048
#> 2 SpaNorm slice1 1000 0.2700809 0.4334076 0.3461446 0.5794992 -0.002975939
#>     Overall n_asw ASW_sampled gene_selection
#> 1 0.5305656  1000       FALSE            all
#> 2 0.4530171  1000       FALSE            all
```
