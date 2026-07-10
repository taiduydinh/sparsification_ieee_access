# On the Impact of Data Sparsification on Model Selection and Learning Performance

This repository contains the source code, experimental notebooks, datasets, and supporting materials for the manuscript:

> **Huiyi Xia and Tai Dinh, “On the Impact of Data Sparsification on Model Selection and Learning Performance.”**  
> Manuscript submitted to *IEEE Access*.

## Overview

This study investigates how feature-wise data sparsification affects model-selection behavior and clustering performance.

Rather than treating sparsification only as a method for reducing representation density or computational cost, the study examines how transforming an original design matrix

\[
\mathbf{X}\in\mathbb{R}^{n\times p}
\]

into a sparse expanded representation

\[
\mathbf{X}_s\in\mathbb{R}^{n\times p_s},
\qquad p_s>p,
\]

changes the relationships among features and influences the behavior of learning algorithms.

The number of observations remains unchanged during the transformation. Each original feature is represented through a collection of sparse component features, resulting in an expanded matrix containing many zero entries.

The experiments cover:

- regression-based model selection using Lasso, Lars, and Glmnet;
- comparisons of coefficient-entry paths and final coefficient patterns;
- synthetic experiments using original and sparsified representations;
- clustering validation using ten UCI benchmark datasets;
- clustering analysis of Chinese housing-price data;
- comparison of original and sparsified representations using external and internal clustering metrics; and
- runtime evaluation.

## Research Objectives

The main objectives of this study are to:

1. examine how feature-wise sparsification changes the structure of a design matrix;
2. investigate whether sparsification affects coefficient-entry behavior in Lasso, Lars, and Glmnet;
3. distinguish between final-model agreement and coefficient-path agreement;
4. evaluate whether sparsification can improve clustering performance in selected datasets;
5. examine the influence of sparsification on feature correlation and structural separability; and
6. determine whether sparsification changes computational runtime.

The study does not claim that sparsification universally improves prediction, clustering, or runtime. Its effects are evaluated empirically and may vary depending on the dataset, feature structure, correlation pattern, and sparsification configuration.

## Experimental Workflow

The experimental workflow consists of the following stages:

1. **Original data representation**

   The input data are represented by an original design matrix  
   \(\mathbf{X}\in\mathbb{R}^{n\times p}\).

2. **Feature-wise sparsification**

   Each original feature is transformed into sparse component features while preserving the same \(n\) observations.

3. **Sparse expanded representation**

   The transformation produces  
   \(\mathbf{X}_s\in\mathbb{R}^{n\times p_s}\), where \(p_s>p\).

4. **Regression-based analysis**

   Lasso, Lars, and Glmnet are applied to the original and sparsified representations. Their coefficient paths, variable-entry orders, and final selected models are compared.

5. **Clustering-based analysis**

   \(k\)-means clustering is applied to the original and sparsified representations.

6. **Performance evaluation**

   The representations are evaluated using model-selection agreement, clustering metrics, visualization, correlation analysis, and runtime measurements.

## Repository Contents

The main experimental notebooks are described below.

| File | Description |
|---|---|
| `regression_figures_r_notebook.ipynb` | Generates the regression and coefficient-path results for Lasso, Lars, and Glmnet using the Chinese housing-price data and synthetic examples. |
| `regression_figures_clustering_kmeans_sparse_orthogonalized_reduced.ipynb` | Performs feature-wise sparsification, clustering analysis, clustering validation, and visualization for the UCI and Chinese housing datasets. |
| `runtime_comparison_fixed_outputs_runtime_v2.ipynb` | Conducts runtime comparisons for the original and sparsified representations. |
| `README.md` | Provides an overview of the study and instructions for reproducing the experiments. |

Additional data, figures, and output files may be organized into corresponding data and output directories.

## Datasets

### Chinese Housing-Price Data

The Chinese housing dataset contains annual observations from 1997 to 2023.

The housing-price variable is used as the response variable in the regression analysis, while seven economic indicators are used as predictors. The same dataset is also used for exploratory clustering and principal component visualization.

The data were obtained from the *China Statistical Yearbook* series published by the National Bureau of Statistics of China.

Because this dataset contains only 27 annual observations, its regression and clustering results should be interpreted as an empirical case study rather than broad population-level evidence.

### Synthetic Data

The synthetic experiments compare:

- an original compact representation;
- a block-structured representation; and
- a sparse expanded representation.

The synthetic examples are used to examine how changes in feature structure and correlation affect coefficient-entry paths and agreement among Lasso, Lars, and Glmnet.

The small illustrative examples are intended to demonstrate the mechanism of the transformation. Additional simulation settings may be used to examine larger values of \(n\) and \(p\), different correlation structures, and different sparsification configurations.

### UCI Benchmark Data

Ten datasets from the UCI Machine Learning Repository are used for clustering validation.

For each dataset:

- input attributes are separated from the reference class labels;
- numerical features are standardized before clustering;
- sparsification is applied only to the feature representation;
- class labels are not used by the \(k\)-means algorithm;
- the number of clusters is set equal to the number of reference classes for external validation; and
- the reference labels are used only to calculate external evaluation metrics.

Dataset-specific information, including the number of observations, number and types of features, number of reference classes, preprocessing steps, and sparsification parameters, is reported in the manuscript and experimental notebooks.

## Methods

### Regression and Model Selection

The regression-based experiments use:

- multiple linear regression;
- principal component regression;
- Lasso;
- Lars; and
- Glmnet.

The analysis distinguishes between two forms of agreement:

1. **Final-model agreement:** whether the algorithms identify the same active variables or reach similar final coefficient patterns.
2. **Path agreement:** whether variables enter the models in a similar order and whether the intermediate coefficient trajectories are consistent.

This distinction is important because two algorithms may reach the same final solution while following different intermediate regularization paths.

### Clustering

Clustering is performed using \(k\)-means on both the original and sparsified feature representations.

The clustering analysis uses the following external evaluation metrics:

- adjusted Rand index;
- clustering accuracy; and
- purity.

Average silhouette width is used as an internal clustering-quality measure.

Principal component analysis is used only for visualizing the grouping structure and is not used as an external validation measure.

### Runtime Evaluation

Runtime is evaluated separately from learning quality.

The runtime experiments compare:

- the model-selection algorithms;
- regression analysis using original and sparsified representations;
- \(k\)-means clustering on the UCI datasets; and
- \(k\)-means clustering on the Chinese housing dataset.

The runtime results should be interpreted as a secondary observation. Sparsification expands the feature dimension and therefore does not necessarily reduce execution time.

## Requirements

The experiments are provided as Jupyter notebooks using R and Python kernels.

The following software is required:

- Jupyter Notebook or JupyterLab;
- a compatible Python environment;
- a compatible R environment; and
- an R kernel registered with Jupyter for notebooks that use R.

Install the packages imported at the beginning of each notebook before running the experiments.

A typical setup can be started with:

```bash
git clone https://github.com/taiduydinh/sparsification_ieee_access.git
cd sparsification_ieee_access
jupyter lab
```

Alternatively, use:

```bash
jupyter notebook
```

Open the required notebook and run all cells from top to bottom.

## Suggested Execution Order

For reproducing the main results, the notebooks may be executed in the following order:

1. `regression_figures_r_notebook.ipynb`
2. `regression_figures_clustering_kmeans_sparse_orthogonalized_reduced.ipynb`
3. `runtime_comparison_fixed_outputs_runtime_v2.ipynb`

The first notebook generates the regression and model-selection results. The second notebook performs the sparsification and clustering experiments. The third notebook produces the runtime comparisons.

## Reproducibility

To obtain reproducible results:

- use the software and package versions reported in the notebooks;
- run all preprocessing cells before running the model-selection or clustering cells;
- retain the specified random seeds;
- use the same numbers of repeated runs and initializations;
- do not use reference class labels as clustering inputs;
- preserve the original train/test or experimental configuration where applicable; and
- record the hardware and software environment when reproducing runtime results.

Minor runtime differences may occur because of differences in processor speed, memory, operating system, background processes, and package versions.

## Main Outputs

Running the notebooks generates outputs related to:

- Lasso coefficient paths;
- Lars coefficient paths;
- Glmnet regularization paths;
- original and sparsified design matrices;
- feature-correlation comparisons;
- model-selection agreement measures;
- UCI clustering evaluation;
- Chinese housing clustering analysis;
- average silhouette width;
- principal component visualizations; and
- runtime comparisons.

## Interpretation of Results

The results should be interpreted within the scope of the tested datasets and experimental configurations.

The study provides evidence that sparsification:

- can alter dependencies among features;
- can change variable-entry behavior;
- can improve agreement among model-selection algorithms in selected settings;
- may improve clustering performance for some datasets; and
- does not uniformly reduce runtime.

The results do not establish that sparsification is universally beneficial. Its effect depends on the original data structure, feature correlations, transformation parameters, learning algorithm, and evaluation criterion.

## Citation

The complete bibliographic information will be added after publication.

Until then, this repository may be cited as:

```text
Huiyi Xia and Tai Dinh,
“On the Impact of Data Sparsification on Model Selection and Learning Performance,”
manuscript submitted to IEEE Access, 2026.
```
