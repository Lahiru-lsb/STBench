# Example normalised spatial transcriptomics datasets

Normalisation results generated from \`spe_example\` using the STBench
\`normalize_spe()\` function.

## Format

A named list of SpatialExperiment objects.

## Source

Derived from the STARmap PLUS mouse brain dataset available through the
Bioconductor STexampleData package.

## Details

Two normalisation methods are included: \`None\`, representing the
unnormalised baseline, and \`SpaNorm\`, representing spatially aware
normalisation.

The original cell-type and tissue-region annotations are retained for
downstream benchmarking.
