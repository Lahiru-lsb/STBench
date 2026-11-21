# Rank normalisation methods by overall clustering agreement

Methods are ranked using the Overall score, calculated as the mean of
NMI, HOM and COM.

## Usage

``` r
rank_normalization_methods(metrics_df)
```

## Arguments

- metrics_df:

  Data frame from calculate_clustering_metrics().

## Value

Data frame containing Rank, method and Overall. \#' @examples
data(norm_example)

banksy_norm \<- run_banksy_individual( norm_list = norm_example, seed =
123 )

metrics_df \<- calculate_clustering_metrics( norm_list = banksy_norm,
ground_truth_col = "cell_type" )

ranking_df \<- rank_normalization_methods( metrics_df = metrics_df )

ranking_df
