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
#> 944 cells/spots sampled to fit model
#> iter:  1, estimating gene-wise dispersion
#> iter:  1, log-likelihood: -22181.157895
#> iter:  1, fitting NB model
#> iter:  1, iter:  1, log-likelihood: -22181.157895
#> iter:  1, iter:  2, log-likelihood: -19613.199517
#> iter:  1, iter:  3, log-likelihood: -18219.054127
#> iter:  1, iter:  4, log-likelihood: -17530.854099
#> iter:  1, iter:  5, log-likelihood: -17258.591876
#> iter:  1, iter:  6, log-likelihood: -17042.133075
#> iter:  1, iter:  7, log-likelihood: -16974.387651
#> iter:  1, iter:  8, log-likelihood: -16945.514715
#> iter:  1, iter:  9, log-likelihood: -16929.551645
#> iter:  1, iter: 10, log-likelihood: -16925.970771
#> iter:  1, iter: 10, log-likelihood: -16925.970771
#> iter:  1, iter: 10, log-likelihood: -16925.970771
#> iter:  1, iter: 11, log-likelihood: -16925.970771 (converged)
#> iter:  2, estimating gene-wise dispersion
#> iter:  2, log-likelihood: -16708.424245
#> iter:  2, fitting NB model
#> iter:  2, iter:  1, log-likelihood: -16708.424245
#> iter:  2, iter:  2, log-likelihood: -16678.838548
#> iter:  2, iter:  2, log-likelihood: -16678.838548
#> iter:  2, iter:  2, log-likelihood: -16678.838548
#> iter:  2, iter:  3, log-likelihood: -16678.838548 (converged)
#> iter:  3, estimating gene-wise dispersion
#> iter:  3, log-likelihood: -16670.914894
#> iter:  3, fitting NB model
#> iter:  3, iter:  1, log-likelihood: -16670.914894
#> iter:  3, iter:  1, log-likelihood: -16670.914894
#> iter:  3, iter:  1, log-likelihood: -16670.914894
#> iter:  3, iter:  2, log-likelihood: -16670.914894
#> iter:  3, iter:  2, log-likelihood: -16670.914894
#> iter:  3, iter:  2, log-likelihood: -16670.914894
#> iter:  3, iter:  3, log-likelihood: -16670.914894 (converged)
#> iter:  4, estimating gene-wise dispersion
#> iter:  4, log-likelihood: -16670.914894
#> iter:  4, fitting NB model
#> iter:  4, iter:  1, log-likelihood: -16670.914894
#> iter:  4, iter:  1, log-likelihood: -16670.914894
#> iter:  4, iter:  1, log-likelihood: -16670.914894
#> iter:  4, iter:  2, log-likelihood: -16670.914894
#> iter:  4, iter:  2, log-likelihood: -16670.914894
#> iter:  4, iter:  2, log-likelihood: -16670.914894
#> iter:  4, iter:  3, log-likelihood: -16670.914894 (converged)
#> iter:  5, log-likelihood: -16670.914894 (converged)
#> (2/2) Normalising data
#> norm_spanorm completed in 0.053 mins
```
