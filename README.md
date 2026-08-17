# On the Impact of Data Sparsification on Model Selection and Learning Performance

This repository contains the source code, experimental notebooks, datasets, numerical outputs, and supporting materials for the manuscript:

> **Huiyi Xia and Tai Dinh, “On the Impact of Data Sparsification on Model Selection and Learning Performance.”**  
> Manuscript submitted to *IEEE Access*.

## Overview

This study investigates how feature-wise data sparsification affects model-selection behavior and clustering performance.

Rather than treating sparsification only as a method for reducing representation density or computational cost, the study examines how an original design matrix

\[
\mathbf{X} \in \mathbb{R}^{n \times p}
\]

is transformed into a sparse expanded representation

\[
\mathbf{X}_s \in \mathbb{R}^{n \times p_s},
\qquad p_s > p.
\]

The transformation changes the feature representation and the relationships among features while preserving the same number of observations.

Each original feature is represented through a collection of sparse component features, resulting in an expanded matrix containing many zero entries.

The experiments cover:

- regression-based model selection using Lasso, Lars, and Glmnet;
- comparisons of coefficient-entry paths and final coefficient patterns;
- illustrative synthetic experiments using original and sparsified representations;
- an extended Monte Carlo study of path agreement, support recovery, and prediction error;
- clustering validation using ten UCI benchmark datasets;
- clustering analysis of Chinese housing-price data;
- comparison of original and sparsified representations using external and internal clustering metrics; and
- a secondary runtime comparison for repeated UCI \(k\)-means experiments.

## Research Objectives

The main objectives of this study are to:

1. examine how feature-wise sparsification changes the structure of a design matrix;
2. investigate whether sparsification affects coefficient-entry behavior in Lasso, Lars, and Glmnet;
3. distinguish between final-model agreement and coefficient-path agreement;
4. evaluate path agreement, support recovery, and predictive error across controlled Monte Carlo settings;
5. evaluate whether sparsification can improve clustering performance in selected datasets;
6. examine the influence of sparsification on feature relationships and correlation structure; and
7. determine whether sparsification changes computational runtime in the repeated UCI \(k\)-means analysis.

The study does not claim that sparsification universally improves prediction, clustering, model-selection agreement, or runtime. Its effects are evaluated empirically and may vary depending on sample size, feature dimension, correlation structure, dataset, learning algorithm, and sparsification configuration.

## Repository Structure

The repository is organized as follows:

```text
sparsification_ieee_access/
├── data/
├── outputs/
├── extended_monte_carlo_model_selection.ipynb
├── regression_figures_clustering_repeated_runs.ipynb
├── regression_figures_r_notebook.ipynb
├── README.md
├── LICENSE
└── .gitattributes
```

The `data/` directory contains the datasets and input files used by the notebooks.

The `outputs/` directory contains saved numerical results and generated analysis outputs used to reproduce the manuscript tables and figures.

## Main Experimental Notebooks

| File | Purpose |
|---|---|
| `regression_figures_r_notebook.ipynb` | Generates the Chinese housing regression and coefficient-path results and the illustrative synthetic examples for Lasso, Lars, and Glmnet. |
| `extended_monte_carlo_model_selection.ipynb` | Implements the extended Monte Carlo study, including the simulation design, sparsification configurations, random-seed specification, path-agreement calculations, support-recovery F1, test RMSE, and the numerical summaries/figure reported from the simulation study. |
| `regression_figures_clustering_repeated_runs.ipynb` | Performs the repeated UCI and Chinese housing clustering analyses, repeated-run summaries, clustering figures, PCA visualizations, and the secondary UCI \(k\)-means runtime comparison. |
| `README.md` | Documents the repository structure and how the analyses map to the manuscript. |

The filenames above correspond to the files currently provided in the repository.

## Reproducibility Map

The following table identifies where the main reproducibility materials are located.

| Reproducibility item | Location |
|---|---|
| Extended Monte Carlo implementation | `extended_monte_carlo_model_selection.ipynb` |
| Monte Carlo simulation configuration | Configuration/setup cells in `extended_monte_carlo_model_selection.ipynb` |
| Monte Carlo random seeds | Seed definitions in `extended_monte_carlo_model_selection.ipynb` |
| Monte Carlo agreement metrics | `extended_monte_carlo_model_selection.ipynb` and saved files in `outputs/` |
| Support-recovery F1 results | `extended_monte_carlo_model_selection.ipynb` and saved files in `outputs/` |
| Test RMSE results | `extended_monte_carlo_model_selection.ipynb` and saved files in `outputs/` |
| Monte Carlo numerical summaries and figure data | `outputs/` |
| Chinese housing regression/path analysis | `regression_figures_r_notebook.ipynb` |
| Repeated UCI clustering | `regression_figures_clustering_repeated_runs.ipynb` |
| Chinese housing clustering/PCA analysis | `regression_figures_clustering_repeated_runs.ipynb` |
| Repeated-run clustering summaries | `regression_figures_clustering_repeated_runs.ipynb` and `outputs/` |
| Secondary UCI \(k\)-means runtime analysis | `regression_figures_clustering_repeated_runs.ipynb` |
| Software/package version information | Environment/version output cells in the executed notebooks |

For reproducibility, the executable notebooks are the authoritative source for the exact parameter values, seed values, algorithm settings, and package versions used in the reported analyses. These values should not be changed when reproducing the manuscript results.

## Datasets

### Chinese Housing-Price Data

The Chinese housing dataset contains annual observations from 1997 to 2023.

The housing-price variable is used as the response variable in the regression analysis, while seven economic indicators are used as predictors. The same dataset is also used for exploratory clustering and principal component visualization.

The data were obtained from the *China Statistical Yearbook* series published by the National Bureau of Statistics of China.

Because this dataset contains only 27 annual observations, its regression and clustering results are treated as a small-sample empirical case study rather than as evidence for causal, forecasting, or stable-regime conclusions.

### Illustrative Synthetic Data

The initial synthetic examples compare:

- an original compact representation;
- a block-structured representation; and
- a sparse expanded representation.

These examples illustrate how changes in feature representation and correlation can affect coefficient-entry paths and agreement among Lasso, Lars, and Glmnet.

### Extended Monte Carlo Study

The extended Monte Carlo evaluation is implemented in:

```text
extended_monte_carlo_model_selection.ipynb
```

The notebook contains the complete executable simulation workflow used for the manuscript, including:

- data-generating settings;
- dimensional configurations;
- correlation structures;
- sparsification schemes;
- random-seed definitions;
- construction of original and sparsified representations;
- Lasso, Lars, and Glmnet path fitting;
- parent-feature entry-order calculations;
- active-set agreement calculations at matched model sizes;
- support-recovery F1;
- test RMSE; and
- generation/export of the numerical summaries and figure data.

The exact parameter values and seed values are defined in the notebook rather than duplicated manually in this README, so that the executable analysis remains the single authoritative specification.

Saved numerical outputs underlying the reported Monte Carlo results are retained in the `outputs/` directory.

### UCI Benchmark Data

Ten datasets from the UCI Machine Learning Repository are used for clustering validation.

For each dataset:

- input attributes are separated from the reference class labels;
- identifier/nonpredictive fields are removed where applicable;
- missing numerical values are median-imputed and nonnumeric values are mode-imputed where needed;
- categorical predictors are expanded before clustering;
- zero-variance columns are removed;
- numerical columns are standardized;
- sparsification is applied only to the feature representation;
- class labels are not supplied to the \(k\)-means algorithm;
- the number of clusters is set equal to the number of reference classes for external validation; and
- reference labels are used only to calculate external evaluation metrics.

Dataset-specific information is reported in the manuscript and the clustering notebook.

## Methods

### Regression and Model Selection

The regression-based experiments use multiple linear regression, principal component regression, Lasso, Lars, and Glmnet as appropriate to the corresponding analysis.

For the regularization-path comparisons:

- Lasso and Lars are fitted using the implementations documented in the notebooks;
- Glmnet is used as the Glmnet implementation of Lasso in the reported regression comparisons;
- the exact path settings used for each reported experiment are specified in the executable notebooks; and
- original and sparsified representations are evaluated using the same documented experimental protocol for each comparison.

The analysis distinguishes between two concepts:

1. **Final-model agreement:** whether the algorithms reach the same selected feature set and, where directly comparable, the same final coefficient pattern.
2. **Path agreement:** similarity in parent-feature entry order and active parent-feature sets at matched intermediate model sizes.

The extended Monte Carlo study formally evaluates path agreement rather than relying on terminal path agreement.

### Clustering

Clustering is performed with \(k\)-means on both the original and sparsified feature representations.

For the repeated clustering experiments, the notebooks retain the complete initialization and random-seed logic used in the manuscript. Each repetition is applied to the same fixed dataset, so the repeated-run intervals quantify **algorithmic variability caused by random initialization**, not observation-level sampling uncertainty or generalization uncertainty.

The clustering analyses report:

- adjusted Rand index;
- clustering accuracy;
- purity; and
- average silhouette width where applicable.

Principal component analysis is used only for visualization of the grouping structure.

### Runtime Evaluation

Runtime is treated as a secondary analysis.

The current manuscript reports the repeated UCI \(k\)-means runtime comparison for original and sparsified representations. The corresponding analysis is contained in:

```text
regression_figures_clustering_repeated_runs.ipynb
```

Because sparsification expands the feature dimension, no general computational advantage is assumed or claimed.

## Software Environment and Package Versions

The experiments are provided as Jupyter notebooks using R and Python kernels.

To preserve exact reproducibility:

- retain the executed environment/version-information cells in the notebooks;
- use the package versions printed by those cells;
- do not replace the documented package versions with newer releases when reproducing the reported results;
- retain all explicit seed settings and initialization settings; and
- run each notebook from top to bottom in a clean session.

For R-based notebooks, environment information can be checked with commands such as:

```r
R.version.string
sessionInfo()
```

For Python-based notebooks, environment information can be checked with commands such as:

```python
import sys
print(sys.version)
```

and, where appropriate:

```bash
pip freeze
```

The committed executed notebooks and their recorded environment outputs should be treated as the reference environment for this manuscript.

## Running the Repository

Clone the repository:

```bash
git clone https://github.com/taiduydinh/sparsification_ieee_access.git
cd sparsification_ieee_access
```

Start JupyterLab:

```bash
jupyter lab
```

or Jupyter Notebook:

```bash
jupyter notebook
```

Then execute the relevant notebook from top to bottom.

## Suggested Execution Order

For reproducing the analyses in the manuscript, use the following order:

1. `regression_figures_r_notebook.ipynb`
2. `extended_monte_carlo_model_selection.ipynb`
3. `regression_figures_clustering_repeated_runs.ipynb`

The first notebook reproduces the Chinese housing regression/path analysis and illustrative synthetic examples.

The second notebook reproduces the extended Monte Carlo evaluation and exports the associated numerical results.

The third notebook reproduces the repeated clustering analyses, clustering visualizations, Chinese housing PCA results, and the secondary UCI \(k\)-means runtime analysis.

## Reproducibility Checklist

Before comparing reproduced results with the manuscript, verify that:

- [ ] all notebooks are run from a clean kernel/session;
- [ ] all preprocessing cells are executed before model fitting;
- [ ] the random seeds in the notebooks are unchanged;
- [ ] the Monte Carlo configuration values are unchanged;
- [ ] the same sparsification settings are used;
- [ ] the same regularization-path settings are used;
- [ ] reference class labels are never used as clustering inputs;
- [ ] the repeated \(k\)-means initialization settings are unchanged;
- [ ] package versions match the versions recorded in the executed notebooks; and
- [ ] exported numerical results are compared with the corresponding files in `outputs/`.

## Main Outputs

The repository provides or generates outputs related to:

- Lasso coefficient paths;
- Lars coefficient paths;
- Glmnet regularization paths;
- original and sparsified design matrices;
- coefficient-entry comparisons;
- parent-feature entry-order agreement;
- active-set agreement at matched model sizes;
- support-recovery F1;
- test RMSE;
- Monte Carlo summary tables and figure data;
- UCI clustering metrics from repeated runs;
- Chinese housing clustering results;
- average silhouette width;
- PCA visualizations; and
- the secondary UCI \(k\)-means runtime comparison.

Where numerical results are exported during notebook execution, the saved files are stored under `outputs/`.

## Interpretation of Results

The results should be interpreted within the scope of the tested datasets and experimental configurations.

The study provides evidence that sparsification:

- can change dependencies among features and the effective input representation;
- can change coefficient-entry behavior;
- can increase agreement among the examined model-selection implementations in selected simulation settings;
- does not necessarily improve support recovery or predictive RMSE;
- may improve clustering separation for selected datasets and metrics; and
- does not uniformly reduce runtime.

The results do not establish that sparsification is universally beneficial. Its effects depend on sample size, feature dimension, correlation structure, representation design, learning implementation, dataset, and evaluation criterion.

## Limitations

The main limitations include:

- the small number of annual observations in the Chinese housing dataset;
- the illustrative nature of the initial synthetic examples;
- setting-dependent Monte Carlo results;
- dataset- and metric-dependent clustering results;
- the absence of a general theoretical condition guaranteeing improvement from sparsification; and
- the sensitivity of runtime measurements to software, hardware, and implementation details.

These limitations should be considered when interpreting the results.

## Repository Note for the Revised Submission

The repository contents and this README have been checked so that the filenames documented here correspond to the files provided in the repository. In particular, the extended Monte Carlo notebook and its associated numerical outputs are explicitly identified to make the simulation study directly reproducible.

For the resubmission, the repository commit used to generate the manuscript results should be retained unchanged so that the submitted manuscript can be traced to a fixed analysis snapshot.

## Citation

The complete bibliographic information will be added after publication.

Until then, this repository may be cited as:

```text
Huiyi Xia and Tai Dinh,
“On the Impact of Data Sparsification on Model Selection and Learning Performance,”
manuscript submitted to IEEE Access, 2026.
```
