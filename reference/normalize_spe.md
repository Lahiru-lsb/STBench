# Apply multiple normalisation methods

Apply multiple normalisation methods

## Usage

``` r
normalize_spe(
  spe,
  methods = c("none", "scran", "sct", "spanorm", "giotto"),
  params = list()
)
```

## Arguments

- spe:

  A SpatialExperiment object.

- methods:

  Character vector containing normalisation methods.

- params:

  Named list containing method-specific parameters.

## Value

A named list of normalised objects.

## Examples

``` r
data(spe_example)

norm <- normalize_spe(
  spe_example,
  methods = c("None", "SpaNorm"),
  params = list(
    spanorm = list(
      sample_p = 0.15,
      df_tps = 6,
      adj_method = "logpac"
    )
  )
)
#> norm_none completed in 0 mins
#> (1/2) Fitting SpaNorm model
#> Warning: encountered non-positive size factor estimates
#> Warning: 'cleanSizeFactors' is deprecated.
#> Use 'scrapper::sanitizeSizeFactors' instead.
#> See help("Deprecated")
#> Warning: encountered non-positive size factor estimates
#> Warning: 'cleanSizeFactors' is deprecated.
#> Use 'scrapper::sanitizeSizeFactors' instead.
#> See help("Deprecated")
#> Warning: encountered non-positive size factor estimates
#> Warning: 'cleanSizeFactors' is deprecated.
#> Use 'scrapper::sanitizeSizeFactors' instead.
#> See help("Deprecated")
#> 1000 cells/spots sampled to fit model
#> iter:  1, estimating gene-wise dispersion
#> iter:  1, log-likelihood: -54804.070925
#> iter:  1, fitting NB model
#> iter:  1, iter:  1, log-likelihood: -54804.070925
#> iter:  1, iter:  2, log-likelihood: -52042.864054
#> iter:  1, iter:  3, log-likelihood: -50742.201882
#> iter:  1, iter:  4, log-likelihood: -50020.180801
#> iter:  1, iter:  4, log-likelihood: -50020.180801
#> iter:  1, iter:  4, log-likelihood: -50020.180801
#> iter:  1, iter:  5, log-likelihood: -50020.180801 (converged)
#> iter:  2, estimating gene-wise dispersion
#> iter:  2, log-likelihood: -49252.287769
#> iter:  2, fitting NB model
#> iter:  2, iter:  1, log-likelihood: -49252.287769
#> iter:  2, iter:  1, log-likelihood: -49252.287769
#> iter:  2, iter:  1, log-likelihood: -49252.287769
#> iter:  2, iter:  2, log-likelihood: -49252.287769
#> iter:  2, iter:  2, log-likelihood: -49252.287769
#> iter:  2, iter:  2, log-likelihood: -49252.287769
#> iter:  2, iter:  3, log-likelihood: -49252.287769 (converged)
#> iter:  3, estimating gene-wise dispersion
#> iter:  3, log-likelihood: -49252.287769
#> iter:  3, fitting NB model
#> iter:  3, iter:  1, log-likelihood: -49252.287769
#> iter:  3, iter:  1, log-likelihood: -49252.287769
#> iter:  3, iter:  1, log-likelihood: -49252.287769
#> iter:  3, iter:  2, log-likelihood: -49252.287769
#> iter:  3, iter:  2, log-likelihood: -49252.287769
#> iter:  3, iter:  2, log-likelihood: -49252.287769
#> iter:  3, iter:  3, log-likelihood: -49252.287769 (converged)
#> iter:  4, log-likelihood: -49252.287769 (converged)
#> (2/2) Normalising data
#> norm_spanorm completed in 0.028 mins
```
