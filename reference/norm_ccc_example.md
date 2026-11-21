# Example normalised data for cell-cell communication

A larger subset of the publicly available STARmap PLUS mouse brain
dataset, prepared for demonstrating cell-cell communication and Gene
Ontology analysis.

## Format

A named list of SpatialExperiment objects.

## Source

Bioconductor STexampleData package:
<https://bioconductor.org/packages/STexampleData/>

## Details

An initial random subset of 300 genes and 1000 cells was selected using
seed 123. Genes and cells with zero total counts were removed.

Gene symbols were harmonised with the mouse CellChat database where
unambiguous matches were available.

The subset was normalised using \`normalize_spe()\` with the \`None\`
and \`SpaNorm\` methods.

Original cell-type and tissue-region annotations are retained for
downstream analyses.
