# Run spatially variable gene detection

Run spatially variable gene detection

## Usage

``` r
run_svg(norm_list, method = "nnSVG", ...)
```

## Arguments

- norm_list:

  Named list of normalised SpatialExperiment objects.

- method:

  SVG detection method.

- ...:

  Additional parameters passed to the SVG method.

## Value

Named list containing SVG results.

## Examples

``` r
data(norm_example)

svg_results <- run_svg(
  norm_list = norm_example,
  method = "nnSVG",
  n_threads = 1,
  verbose = FALSE
)

names(svg_results)
#> [1] "None"    "SpaNorm"
head(as.data.frame(
  SummarizedExperiment::rowData(svg_results[[1]])
))
#>             sigma.sq     tau.sq      phi     loglik runtime       mean
#> HSPB7   0.0003975458 0.02686554 25.55649  360.89289   0.216 0.03561908
#> KCNC3   0.0641103501 0.16974652 33.42317 -632.78653   0.297 0.24149342
#> COL25A1 0.0079245734 0.07710991 20.38098 -170.58832   0.315 0.09589966
#> MAL     0.1872068444 0.23637473 36.37872 -890.05252   0.280 0.36704269
#> CPXM2   0.0004492348 0.05014129 74.15860   68.97299   0.220 0.05788464
#> TM4SF4  0.0001479891 0.01503106 73.53679  637.19087   0.297 0.01878617
#>                var     spcov     prop_sv  loglik_lm    LR_stat rank
#> HSPB7   0.02729862 0.5597716 0.014581833  360.65616  0.4734607   33
#> KCNC3   0.23457624 1.0484767 0.274143544 -654.58969 43.6063223    6
#> COL25A1 0.08512410 0.9282627 0.093192466 -176.13722 11.0977924   15
#> MAL     0.42515362 1.1788113 0.441961731 -935.27388 90.4427303    2
#> CPXM2   0.05062784 0.3661620 0.008879819   69.11804 -0.2901053   48
#> TM4SF4  0.01519245 0.6475548 0.009749557  637.26597 -0.1501894   44
#>                 pval         padj
#> HSPB7   7.892040e-01 1.000000e+00
#> KCNC3   3.396311e-10 2.830259e-09
#> COL25A1 3.891751e-03 1.297250e-02
#> MAL     0.000000e+00 0.000000e+00
#> CPXM2   1.000000e+00 1.000000e+00
#> TM4SF4  1.000000e+00 1.000000e+00
```
