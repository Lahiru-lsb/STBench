# SpaNorm normalisation

SpaNorm normalisation

## Usage

``` r
norm_spanorm(
  spe,
  sample_p = NULL,
  df_tps = 6,
  adj_method = "logpac",
  seed = 123,
  ...
)
```

## Arguments

- spe:

  A SpatialExperiment object.

- sample_p:

  Sampling proportion. If NULL, 3000/ncol(spe) is used.

- df_tps:

  Degrees of freedom for thin-plate spline.

- adj_method:

  Adjustment method.

- seed:

  Random seed.

- ...:

  Additional arguments passed to SpaNorm.

## Value

Normalised object.
