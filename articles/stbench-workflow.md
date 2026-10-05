# STBench: Benchmarking Normalisation Methods for Spatial Transcriptomics

------------------------------------------------------------------------

## Overview

`STBench` provides a unified framework for applying and benchmarking
normalisation methods for spatial transcriptomics data.

The package supports a workflow including:

- quality control;
- normalisation;
- spatially variable gene analysis;
- spatial expression visualisation;
- gene-set benchmarking;
- cell-type annotation;
- spatial clustering;
- clustering performance evaluation; and
- gene ontology enrichment analysis.

This vignette demonstrates a typical `STBench` workflow using a
`SpatialExperiment` object.

## Installation

The development version of `STBench` can be installed from GitHub.

``` r

# install.packages("remotes")
# remotes::install_github("USERNAME/STBench")
```

Load the package with:

``` r

library(STBench)
```

Depending on the analyses performed, additional packages may also be
required.

``` r

library(SpatialExperiment)
library(SummarizedExperiment)
```

## Input data

`STBench` primarily works with `SpatialExperiment` objects containing a
count matrix and spatial coordinates.

For this vignette, we assume that an object called `spe` has already
been loaded.

``` r

spe
```

The object should contain raw counts in the `counts` assay.

``` r

assayNames(spe)
```

For computational efficiency when experimenting with a new workflow,
users may initially work with a subset of genes or spots.

``` r

spe <- spe[1:500, 1:2000]
```

## Quality control

### Calculate QC metrics

Basic quality-control metrics can be calculated using
`add_qc_metrics()`.

``` r

spe_qc <- add_qc_metrics(
  spe = spe,
  assay_name = "counts",
  mito_pattern = "^MT-"
)
```

The resulting object contains additional QC information that can be used
for visualisation and filtering.

### Visualise QC distributions

QC distributions can be inspected with `plot_qc()`.

``` r

qc <- plot_qc(
  spe = spe_qc,
  bins = 45,
  show_density = TRUE,
  theme_name = "classic"
)

qc$plot
```

Individual QC panels can also be accessed separately.

``` r

qc$plots$library_size
qc$plots$gene_mean
qc$plots$detected_genes
qc$plots$mitochondrial
```

### Explore QC cutoffs

Potential filtering thresholds can be examined before removing
observations.

``` r

cut <- plot_qc_cutoffs(
  spe = spe_qc,
  library_cutoff = NULL,
  gene_cutoff = NULL,
  n_points = 200,
  theme_name = "classic"
)

cut$plot
```

Candidate thresholds can then be supplied directly.

``` r

cut_selected <- plot_qc_cutoffs(
  spe = spe_qc,
  library_cutoff = 2.5,
  gene_cutoff = 0.2,
  n_points = 200,
  theme_name = "classic"
)

cut_selected$plot
```

### Apply QC filtering

Filtering is performed using `filter_qc()`.

``` r

spe_filtered <- filter_qc(
  spe = spe_qc,
  library_cutoff = 2.5,
  gene_cutoff = 0.01,
  recalculate = TRUE,
  assay_name = "counts",
  mito_pattern = "^MT-"
)
```

QC distributions can then be reassessed after filtering.

``` r

qc_after <- plot_qc(
  spe = spe_filtered,
  bins = 45,
  show_density = TRUE,
  theme_name = "classic"
)

qc_after$plot
```

For downstream analyses we use the filtered object.

``` r

spe_use <- spe_filtered
```

## Normalisation

Multiple normalisation methods can be applied through a common interface
using
[`normalize_spe()`](https://lahiru-lsb.github.io/STBench/reference/normalize_spe.md).

``` r

norm <- normalize_spe(
  spe = spe_use,
  methods = c(
    "none",
    "scran"
  )
)

names(norm)
```

The output is a named list containing the corresponding normalised
`SpatialExperiment` objects.

Additional normalisation methods can be included when their required
packages are installed.

## Spatially variable gene analysis

### Detect spatially variable genes

Spatially variable genes can be identified using
[`run_svg()`](https://lahiru-lsb.github.io/STBench/reference/run_svg.md).

``` r

svg <- run_svg(
  norm_list = norm,
  method = "nnSVG",
  verbose = TRUE
)

names(svg)
```

For illustration, select a small collection of genes.

``` r

genes_use <- rownames(spe_use)[1:5]
```

### Compare SVG statistics

SVG statistics can be compared across normalisation methods.

``` r

svg_stat <- plot_svg_stat(
  svg_norm = svg,
  genes = genes_use,
  stat = "LR_stat",
  transform = "log"
)

svg_stat$plot
```

### Compare SVG ranks

The corresponding SVG ranks can also be visualised.

``` r

svg_rank <- plot_svg_rank(
  svg,
  genes = genes_use
)

svg_rank$plot
```

## Spatial expression visualisation

Spatial expression patterns can be compared across normalisation methods
using
[`plot_spatial_expression()`](https://lahiru-lsb.github.io/STBench/reference/plot_spatial_expression.md).

### Scaled expression

Expression values can be scaled to facilitate comparison of spatial
patterns.

``` r

p_scaled <- plot_spatial_expression(
  norm_list = norm,
  genes = genes_use,
  assay_name = "logcounts",
  scale_expr = TRUE,
  point_size = 0.5,
  colour_option = "magma",
  theme_name = "classic"
)

p_scaled$plot
```

### Unscaled expression

Original normalised expression values can also be displayed.

``` r

p_original <- plot_spatial_expression(
  norm_list = norm,
  genes = genes_use,
  assay_name = "logcounts",
  scale_expr = FALSE,
  point_size = 0.5,
  colour_option = "magma",
  ncol_genes = 1,
  theme_name = "classic"
)

p_original$plot
```

## Gene-set benchmarking

Known gene sets can be used to evaluate how different normalisation
methods affect SVG detection.

### Distribution of SVG statistics

For example, a set of housekeeping or stable genes can be examined.

``` r

stable <- plot_svg_gene_set_distribution(
  svg,
  genes = Housekeeping_Genes$Gene.name,
  stat = "LR_stat",
  transform = "log",
  plot_type = "boxplot"
)

stable$plot
```

### Gene-set representation among top SVGs

The proportion of genes from a selected gene set among the
highest-ranked SVGs can also be calculated.

``` r

topn <- plot_svg_topn_gene_set(
  svg_list = svg,
  genes = Housekeeping_Genes$Gene.name,
  top_n = c(
    10,
    20,
    50,
    100
  )
)

topn$plot
```

## Cell-type annotation

Cell-type annotation can be performed for each normalisation method
using
[`run_annotation()`](https://lahiru-lsb.github.io/STBench/reference/run_annotation.md).

A suitable reference dataset and corresponding cell-type labels must
first be provided.

``` r

annotation_results <- run_annotation(
  norm_list = norm,
  ref = ref,
  labels = ref$cell_type_spec,
  de.method = "wilcox"
)
```

### Spatial annotation maps

``` r

p_annotation <- plot_spatial_annotation(
  annotation_list = annotation_results,
  label_col = "SingleR_label",
  ncol = 2
)

p_annotation$plot
```

### Cell-type proportions

``` r

p_celltype <- plot_celltype_proportion(
  annotation_list = annotation_results,
  label_col = "SingleR_label"
)

p_celltype$plot
```

### Annotation agreement

Agreement in cell-type assignments across normalisation methods can be
assessed using:

``` r

p_agree <- plot_annotation_agreement(
  norm_list = annotation_results,
  annotation_col = "SingleR_label"
)

p_agree$plot
```

## Spatial clustering

`STBench` provides an interface for running BANKSY independently for
each normalisation method.

``` r

banksy_norm <- run_banksy_individual(
  norm_list = norm,
  cluster_col = "banksy_cluster",
  k_geom = 15,
  lambda = 0.8,
  resolution = 0.2,
  seed = 123
)
```

Cluster assignments can be inspected directly.

``` r

table(banksy_norm$none$banksy_cluster)
table(banksy_norm$scran$banksy_cluster)
```

### Spatial clustering maps

``` r

cluster_plot <- plot_spatial_clustering(
  norm_list = banksy_norm,
  cluster_col = "banksy_cluster",
  method_order = c(
    "none",
    "scran"
  ),
  point_size = 0.5
)

cluster_plot$plot
```

## Clustering performance

When ground-truth biological labels are available, clustering
performance can be quantified using the Adjusted Rand Index (ARI).

### Calculate ARI

``` r

ari_results <- calculate_ari(
  norm_list = banksy_norm,
  ground_truth_col = "layer_guess",
  cluster_col = "banksy_cluster"
)

ari_results
```

### Visualise ARI

``` r

ari_plot <- plot_ari(
  ari_df = ari_results,
  method_order = c(
    "none",
    "scran"
  )
)

ari_plot$plot
```

Higher ARI values indicate greater agreement between the inferred
spatial clusters and the supplied reference labels.

## Gene ontology enrichment

Cluster-specific marker genes can be identified and used for downstream
Gene Ontology enrichment analysis.

The appropriate organism annotation package must be supplied through
`OrgDb`.

``` r

go_results <- calculate_go(
  norm_list = banksy_norm,
  cluster_col = "banksy_cluster",
  methods = c(
    "none",
    "scran"
  ),
  OrgDb = org.Hs.eg.db::org.Hs.eg.db
)
```

### Marker genes

The top marker genes used for enrichment analysis can be visualised
with:

``` r

go_genes_plot <- plot_go_genes(
  go_results = go_results,
  top_n = 5,
  method_order = c(
    "none",
    "scran"
  )
)

go_genes_plot$plot
```

### GO enrichment results

``` r

go_plot <- plot_go(
  go_results = go_results,
  top_n = 5,
  method_order = c(
    "none",
    "scran"
  )
)

go_plot$plot
```

## Summary

`STBench` provides a consistent workflow for comparing normalisation
methods across several downstream spatial transcriptomics analyses.

A typical analysis consists of:

1.  performing quality control;
2.  applying one or more normalisation methods;
3.  detecting spatially variable genes;
4.  examining spatial expression patterns;
5.  benchmarking predefined gene sets;
6.  evaluating cell-type annotations;
7.  performing spatial clustering;
8.  comparing clustering accuracy; and
9.  assessing cluster-specific biological enrichment.

The same framework allows results from different normalisation
approaches to be generated and compared using a common interface.

## Session information

``` r

sessionInfo()
#> R version 4.6.1 (2026-06-24)
#> Platform: x86_64-pc-linux-gnu
#> Running under: Ubuntu 24.04.5 LTS
#> 
#> Matrix products: default
#> BLAS:   /usr/lib/x86_64-linux-gnu/openblas-pthread/libblas.so.3 
#> LAPACK: /usr/lib/x86_64-linux-gnu/openblas-pthread/libopenblasp-r0.3.26.so;  LAPACK version 3.12.0
#> 
#> locale:
#>  [1] LC_CTYPE=C.UTF-8       LC_NUMERIC=C           LC_TIME=C.UTF-8       
#>  [4] LC_COLLATE=C.UTF-8     LC_MONETARY=C.UTF-8    LC_MESSAGES=C.UTF-8   
#>  [7] LC_PAPER=C.UTF-8       LC_NAME=C              LC_ADDRESS=C          
#> [10] LC_TELEPHONE=C         LC_MEASUREMENT=C.UTF-8 LC_IDENTIFICATION=C   
#> 
#> time zone: UTC
#> tzcode source: system (glibc)
#> 
#> attached base packages:
#> [1] stats     graphics  grDevices utils     datasets  methods   base     
#> 
#> other attached packages:
#> [1] STBench_0.1.0
#> 
#> loaded via a namespace (and not attached):
#>  [1] digest_0.6.39     desc_1.4.3        R6_2.6.1          fastmap_1.2.0    
#>  [5] xfun_0.61         cachem_1.1.0      knitr_1.52        htmltools_0.5.9  
#>  [9] rmarkdown_2.32    lifecycle_1.0.5   cli_3.6.6         sass_0.4.10      
#> [13] pkgdown_2.2.1     textshaping_1.0.5 jquerylib_0.1.4   systemfonts_1.3.2
#> [17] compiler_4.6.1    tools_4.6.1       ragg_1.5.2        bslib_0.12.0     
#> [21] evaluate_1.0.5    yaml_2.3.12       otel_0.2.0        jsonlite_2.0.0   
#> [25] rlang_1.3.0       fs_2.1.0          htmlwidgets_1.6.4
```
