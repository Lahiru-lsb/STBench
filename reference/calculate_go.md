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
