# SCTransform normalisation

SCTransform normalisation

## Usage

``` r
norm_sct(spe, seed = 123, vst_flavor = "v2", verbosity = 1, ...)
```

## Arguments

- spe:

  A SpatialExperiment or SingleCellExperiment object.

- seed:

  Random seed.

- vst_flavor:

  SCTransform vst flavour.

- verbosity:

  Verbosity passed to sctransform.

- ...:

  Additional arguments passed to sctransform::vst().

## Value

Normalised object.
