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
if (FALSE) { # \dontrun{
norm <- normalize_spe(
  spe,
  methods = c("none", "scran")
)
} # }
```
