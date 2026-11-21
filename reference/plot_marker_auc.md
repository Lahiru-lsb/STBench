# Plot marker-gene discrimination across methods

Calculate ROC AUC for marker genes across normalisation methods using
target cell-type labels.

## Usage

``` r
plot_marker_auc(
  norm_list,
  markers,
  target_types,
  annotation_col = "SingleR_label",
  method_order = NULL,
  reference_method = NULL,
  palette = "viridis",
  point_size = 3,
  theme_name = "classic",
  ncol = 2
)
```

## Arguments

- norm_list:

  Named list of SpatialExperiment objects.

- markers:

  Character vector of marker genes.

- target_types:

  Named character vector mapping marker genes to their expected target
  cell types.

- annotation_col:

  Cell-type annotation column.

- method_order:

  Optional normalisation method order.

- reference_method:

  Optional method used to define fixed cell-type labels across methods.

- palette:

  Optional named colour vector or viridis palette name.

- point_size:

  Size of AUC points.

- theme_name:

  Plot theme.

- ncol:

  number of column of the panel

## Value

List containing AUC summary data and ggplot.

## Examples

``` r
data(norm_example)

spe <- norm_example[[1]]

labels <- as.character(
  SummarizedExperiment::colData(spe)$cell_type
)

label_counts <- sort(
  table(labels),
  decreasing = TRUE
)

target_label <- names(label_counts)[1]

markers <- head(rownames(spe), 2)

target_types <- stats::setNames(
  rep(target_label, length(markers)),
  markers
)

p <- plot_marker_auc(
  norm_list = norm_example,
  markers = markers,
  target_types = target_types,
  annotation_col = "cell_type",
  reference_method = "None",
  palette = "magma",
  point_size = 3
)

p$plot
```
