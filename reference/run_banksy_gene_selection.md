# Run BANKSY with different gene-selection strategies

Runs BANKSY clustering independently for each normalisation method using
all genes, highly variable genes (HVGs), or spatially variable genes
(SVGs).

## Usage

``` r
run_banksy_gene_selection(
  norm_list,
  svg_list = NULL,
  methods = names(norm_list),
  gene_selection = c("all", "hvg500", "hvg1000", "svg100", "svg200", "svg500"),
  rank_col = "rank",
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

  Named list of SpatialExperiment objects, or named lists of
  SpatialExperiment slices.

- svg_list:

  Optional named list of SVG results, corresponding to the normalisation
  methods.

- methods:

  Normalisation methods to analyse.

- gene_selection:

  Character vector containing any of "all", "hvg500", "hvg1000",
  "svg100", "svg200", "svg500".

- rank_col:

  Column containing SVG rankings.

- assay_name:

  Assay used for clustering and HVG selection.

- cluster_col:

  Column for BANKSY cluster assignments.

- k_geom:

  Number of spatial neighbours.

- lambda:

  BANKSY spatial weighting parameter.

- resolution:

  Clustering resolution.

- seed:

  Random seed.

## Value

Nested list indexed by normalisation method, then gene-selection
strategy. Each entry contains a clustered SpatialExperiment object or
named slice list.

## Details

HVGs are selected by expression variance within each normalisation
method. SVGs are selected using the gene rankings supplied in svg_list.

## Examples

``` r
data(norm_example)

banksy_genes <- run_banksy_gene_selection(
  norm_list = norm_example,
  methods = names(norm_example),
  gene_selection = "all",
  assay_name = "logcounts",
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
```
