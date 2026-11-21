# Example spatial transcriptomics dataset

A subset of the publicly available STARmap PLUS mouse brain spatial
transcriptomics dataset, obtained using the \`STARmapPLUS_mouseBrain()\`
function from the Bioconductor package \`STexampleData\`.

## Format

A SpatialExperiment object.

## Source

Bioconductor STexampleData package:
<https://bioconductor.org/packages/STexampleData/>

## Details

The dataset was generated using STARmap PLUS, an imaging-based spatial
transcriptomics technology.

A random subset of 100 genes and 200 cells was selected using seed 123.
Genes and cells with zero total counts were removed.

The dataset contains spatial coordinates, raw gene counts, and original
cell-type and tissue-region annotations.

Two additional annotation columns were created: \`cell_type\`,
containing molecular cell-type annotations, and \`layer_guess\`,
containing molecular tissue-region annotations.
