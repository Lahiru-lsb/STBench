# Compare normalised library sizes across methods

Calculate and visualise total normalised expression across spatial
locations for different normalisation methods.

## Usage

``` r
plot_library_size_comparison(
  norm,
  methods = NULL,
  assay_name = "logcounts",
  point_size = 0.5,
  theme_name = "classic"
)
```

## Arguments

- norm:

  Named list of normalised SpatialExperiment objects.

- methods:

  Character vector of methods to compare. If NULL, all methods except
  sctransform and Giotto are used.

- assay_name:

  Name of the log-normalised assay. Default is "logcounts".

- point_size:

  Point size for spatial maps.

- theme_name:

  Plot theme.

## Value

A list containing comparison data, boxplot, spatial plot, and combined
plot.

## Details

Log-normalised expression is back-transformed using expm1(), summed
across genes, and transformed again using log1p().

Produces a boxplot and spatial maps.

By default, sctransform and Giotto are excluded because their
transformed expression values may not represent log1p-transformed
non-negative expression.

## Examples

``` r
data(norm_example)

p_ls <- plot_library_size_comparison(
  norm_example,
  methods = NULL,
  assay_name = "logcounts",
  point_size = 0.5,
  theme_name = "classic"
)

p_ls$plot
```
