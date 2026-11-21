# Calculate GO enrichment from cluster-specific DE genes

Identify cluster-specific differentially expressed genes across
normalisation methods and perform Gene Ontology enrichment for each
cluster.

## Usage

``` r
calculate_go(
  norm_list,
  cluster_col = "banksy_cluster",
  methods = names(norm_list),
  assay_name = "logcounts",
  OrgDb,
  key_type = "SYMBOL",
  ont = "BP",
  fdr_cutoff = 0.05,
  min_prop = 0.7,
  min_spots = 30,
  min_genes = 10,
  pvalue_cutoff = 0.05,
  qvalue_cutoff = 0.05,
  p_adjust_method = "BH",
  test_type = "wilcox",
  readable = TRUE
)
```

## Arguments

- norm_list:

  Named list of normalised SpatialExperiment objects.

- cluster_col:

  Name of the colData column containing cluster assignments.

- methods:

  Optional character vector specifying the normalisation methods to
  analyse.

- assay_name:

  Name of the assay used for differential expression analysis.

- OrgDb:

  Organism annotation database passed to
  \`clusterProfiler::enrichGO()\`.

- key_type:

  Gene identifier type.

- ont:

  Gene Ontology category. One of \`"BP"\`, \`"MF"\`, \`"CC"\`, or
  \`"ALL"\`.

- fdr_cutoff:

  FDR threshold used to define significant cluster-specific DE genes.

- min_prop:

  Minimum proportion passed to \`scran::findMarkers()\`.

- min_spots:

  Minimum number of spatial locations required for a cluster.

- min_genes:

  Minimum number of DE genes required to run GO enrichment.

- pvalue_cutoff:

  GO enrichment p-value cutoff.

- qvalue_cutoff:

  GO enrichment q-value cutoff.

- p_adjust_method:

  Multiple-testing correction method.

- test_type:

  Statistical test used for differential expression analysis in
  \`scran::findMarkers()\`. Default is \`"wilcox"\`.

- readable:

  Logical indicating whether gene IDs should be converted to readable
  symbols.

## Value

A list containing:

- \`markers\`: full marker results for each method.

- \`genes\`: significant DE genes used for GO.

- \`go\`: GO enrichment results.

- \`universe\`: background genes for each method.

## Details

Each normalisation method should contain one SpatialExperiment object
representing the same spatial sample.

## Examples

``` r
data(norm_ccc_example)

go_result <- calculate_go(
  norm_list = norm_ccc_example,
  cluster_col = "layer_guess",
  methods = names(norm_ccc_example),
  assay_name = "logcounts",
  OrgDb = org.Mm.eg.db::org.Mm.eg.db,
  key_type = "SYMBOL",
  ont = "BP",
  fdr_cutoff = 0.05,
  min_prop = 0.4,
  min_spots = 10,
  min_genes = 20,
  pvalue_cutoff = 0.05,
  qvalue_cutoff = 0.05,
  p_adjust_method = "BH",
  readable = TRUE,
  test_type = "t"
)
#> Warning: 'findMarkers' is deprecated.
#> Use 'scrapper::scoreMarkers.se' instead.
#> See help("Deprecated")
#> Warning: 'pairwiseWilcox' is deprecated.
#> See help("Deprecated")
#> Warning: 'combineMarkers' is deprecated.
#> Use 'scrapper::summarizeEffects' instead.
#> See help("Deprecated")
#> 
#> 
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 82.5% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 69.6% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 87.32% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 69.6% of input gene IDs are fail to map...
#> Warning: Skipping GO for method 'None', cluster 'FbTrt': fewer than 20 DE genes.
#> Warning: Skipping GO for method 'None', cluster 'Hbl_VS': fewer than 20 DE genes.
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 80% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 69.6% of input gene IDs are fail to map...
#> Warning: Skipping GO for method 'None', cluster 'L1_HPFmo_Mngs': fewer than 20 DE genes.
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 52.38% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 69.6% of input gene IDs are fail to map...
#> Warning: Skipping GO for method 'None', cluster 'OB_1': fewer than 20 DE genes.
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 54.29% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 69.6% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 69.23% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 69.6% of input gene IDs are fail to map...
#> Warning: 'findMarkers' is deprecated.
#> Use 'scrapper::scoreMarkers.se' instead.
#> See help("Deprecated")
#> Warning: 'pairwiseWilcox' is deprecated.
#> See help("Deprecated")
#> Warning: 'combineMarkers' is deprecated.
#> Use 'scrapper::summarizeEffects' instead.
#> See help("Deprecated")
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 84.21% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 69.6% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 87.88% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 69.6% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 90.91% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 69.6% of input gene IDs are fail to map...
#> Warning: Skipping GO for method 'SpaNorm', cluster 'Hbl_VS': fewer than 20 DE genes.
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 84.21% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 69.6% of input gene IDs are fail to map...
#> Warning: Skipping GO for method 'SpaNorm', cluster 'L1_HPFmo_Mngs': fewer than 20 DE genes.
#> Warning: Skipping GO for method 'SpaNorm', cluster 'LSX_HY_MB_HB': fewer than 20 DE genes.
#> Warning: Skipping GO for method 'SpaNorm', cluster 'OB_1': fewer than 20 DE genes.
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 58.06% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 69.6% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 66.67% of input gene IDs are fail to map...
#> 'select()' returned 1:1 mapping between keys and columns
#> Warning: 69.6% of input gene IDs are fail to map...
```
