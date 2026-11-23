# Run CellChat across normalization methods

Runs CellChat cell-cell communication analysis across multiple
normalized versions of the same SpatialExperiment object.

## Usage

``` r
run_ccc(
  spelist,
  celltype_col,
  database,
  spatial_factors,
  interaction_range,
  contact_range,
  assay_name = "logcounts",
  nboot = 100,
  min_cells = 10,
  trim = 0.1,
  scale_distance = 0.1,
  variable_both = FALSE,
  verbose = TRUE,
  ...
)
```

## Arguments

- spelist:

  Named list of SpatialExperiment objects. Names should correspond to
  normalization methods.

- celltype_col:

  Character. Column in colData(spe) containing cell-type labels.

- database:

  CellChat database object, e.g. CellChatDB.mouse.

- spatial_factors:

  Data frame containing CellChat spatial factors, typically ratio and
  tol.

- interaction_range:

  Numeric. Maximum spatial interaction distance.

- contact_range:

  Numeric. Contact-dependent interaction distance.

- assay_name:

  Character. Assay containing normalized expression. Default is
  "logcounts".

- nboot:

  Integer. Number of bootstrap iterations.

- min_cells:

  Integer. Minimum number of spots/cells per group.

- trim:

  Numeric. Trimming proportion for truncated mean.

- scale_distance:

  Numeric. Distance scaling used by CellChat.

- variable_both:

  Logical. Passed to identifyOverExpressedInteractions().

- verbose:

  Logical. Print progress messages.

- ...:

  Additional arguments.

## Value

Named list containing CellChat results for each method.

## Examples

``` r
if (requireNamespace("CellChat", quietly = TRUE)) {

  data(norm_ccc_example)

  data("CellChatDB.mouse", package = "CellChat")

  ccc_results <- run_ccc(
    spelist = norm_ccc_example,
    celltype_col = "cell_type",
    database = CellChat::CellChatDB.mouse,
    spatial_factors = data.frame(
      ratio = 0.5,
      tol = 12.5
    ),
    interaction_range = 250,
    contact_range = 25,
    assay_name = "logcounts",
    nboot = 10,
    min_cells = 5,
    trim = 0.1,
    scale_distance = 0.1,
    variable_both = FALSE,
    verbose = FALSE
  )

}
#> [1] "Create a CellChat object from a data matrix"
#> Create a CellChat object from spatial transcriptomics data... 
#> Set cell identities for the new CellChat object 
#> The cell groups used for CellChat analysis are  Astrocytes, Cerebellum neurons, Cholinergic and monoaminergic neurons, Choroid plexus epithelial cells, Dentate gyrus granule neurons, Di- and mesencephalon excitatory neurons, Di- and mesencephalon inhibitory neurons, Ependymal cells, Glutamatergic neuroblasts, Hindbrain neurons/Spinal cord neurons, Microglia, Non-glutamatergic neuroblasts, Olfactory inhibitory neurons, Oligodendrocyte precursor cells, Oligodendrocytes, Peptidergic neurons, Pericytes, Perivascular macrophages, Telencephalon inhibitory interneurons, Telencephalon projecting excitatory neurons, Telencephalon projecting inhibitory neurons, Unannotated, Vascular and leptomeningeal cells, Vascular endothelial cells, Vascular smooth muscle cells 
#> The number of highly variable ligand-receptor pairs used for signaling inference is 94 
#> truncatedMean is used for calculating the average gene expression per cell group. 
#> [1] ">>> Run CellChat on spatial transcriptomics data using distances as constraints of the computed communication probability <<< [2026-11-23 01:20:25.006207]"
#> The input L-R pairs have both secreted signaling and contact-dependent signaling. Run CellChat in a contact-dependent manner for `Cell-Cell Contact` signaling, and in a diffusion manner based on the `interaction.range` for other L-R pairs. 
#> [1] ">>> CellChat inference is done. Parameter values are stored in `object@options$parameter` <<< [2026-11-23 01:20:26.750627]"
#> The cell-cell communication related with the following cell groups are excluded due to the few number of cells:  Cerebellum neurons, Dentate gyrus granule neurons, Glutamatergic neuroblasts, Non-glutamatergic neuroblasts, Olfactory inhibitory neurons !     5.2% interactions are removed!
#> [1] "Create a CellChat object from a data matrix"
#> Create a CellChat object from spatial transcriptomics data... 
#> Set cell identities for the new CellChat object 
#> The cell groups used for CellChat analysis are  Astrocytes, Cerebellum neurons, Cholinergic and monoaminergic neurons, Choroid plexus epithelial cells, Dentate gyrus granule neurons, Di- and mesencephalon excitatory neurons, Di- and mesencephalon inhibitory neurons, Ependymal cells, Glutamatergic neuroblasts, Hindbrain neurons/Spinal cord neurons, Microglia, Non-glutamatergic neuroblasts, Olfactory inhibitory neurons, Oligodendrocyte precursor cells, Oligodendrocytes, Peptidergic neurons, Pericytes, Perivascular macrophages, Telencephalon inhibitory interneurons, Telencephalon projecting excitatory neurons, Telencephalon projecting inhibitory neurons, Unannotated, Vascular and leptomeningeal cells, Vascular endothelial cells, Vascular smooth muscle cells 
#> The number of highly variable ligand-receptor pairs used for signaling inference is 93 
#> truncatedMean is used for calculating the average gene expression per cell group. 
#> [1] ">>> Run CellChat on spatial transcriptomics data using distances as constraints of the computed communication probability <<< [2026-11-23 01:20:29.677838]"
#> The input L-R pairs have both secreted signaling and contact-dependent signaling. Run CellChat in a contact-dependent manner for `Cell-Cell Contact` signaling, and in a diffusion manner based on the `interaction.range` for other L-R pairs. 
#> [1] ">>> CellChat inference is done. Parameter values are stored in `object@options$parameter` <<< [2026-11-23 01:20:31.314449]"
#> The cell-cell communication related with the following cell groups are excluded due to the few number of cells:  Cerebellum neurons, Dentate gyrus granule neurons, Glutamatergic neuroblasts, Non-glutamatergic neuroblasts, Olfactory inhibitory neurons !     7.8% interactions are removed!
```
