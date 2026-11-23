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
  BPPARAM = BiocParallel::SerialParam(),
  verbose = FALSE
)

names(svg_results)
#> [1] "None"    "SpaNorm"
head(as.data.frame(
  SummarizedExperiment::rowData(svg_results[[1]])
))
#>        sigma.sq    tau.sq       phi     loglik runtime      mean       var
#> Ptgds 0.5770782 0.7319418 49.012407 -1520.5579   0.385 0.8811459 1.2986705
#> MBP   1.0243742 0.5095626 12.858615 -1386.1035   0.485 1.3962075 1.4765692
#> PLTP  0.1443289 0.5997324 46.666589 -1263.3052   0.356 0.5371881 0.7463753
#> Vtn   0.1023236 0.3686028 70.590268 -1037.5230   0.495 0.2416461 0.4707457
#> Penk  0.1329600 0.4536826  5.762832 -1089.9687   0.275 0.3044798 0.6157458
#> TRF   0.1442528 0.3037294 29.499075  -981.6291   0.358 0.3018491 0.4497358
#>           spcov   prop_sv loglik_lm    LR_stat rank         pval         padj
#> Ptgds 0.8621236 0.4408475 -1549.109  57.101841   33 3.985701e-13 6.038940e-13
#> MBP   0.7249021 0.6678073 -1613.299 454.390846    1 0.000000e+00 0.000000e+00
#> PLTP  0.7072129 0.1939744 -1272.175  17.739365   40 1.405872e-04 1.757340e-04
#> Vtn   1.3237564 0.2172815 -1041.720   8.393259   45 1.504621e-02 1.671801e-02
#> Penk  1.1975731 0.2266457 -1175.978 172.018049   16 0.000000e+00 0.000000e+00
#> TRF   1.2582653 0.3220056 -1018.891  74.523550   29 1.110223e-16 1.914178e-16
```
