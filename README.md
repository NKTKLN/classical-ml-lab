# Classical ML Lab 🧪

[![Python](https://img.shields.io/badge/Python-3.13%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-notebooks-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-baseline-F7931E?logo=scikitlearn&logoColor=white)](https://scikit-learn.org/)
[![uv](https://img.shields.io/badge/uv-managed-DE5FE9?logo=uv&logoColor=white)](https://docs.astral.sh/uv/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE.md)

**English** · [Русский](./README.ru.md)

This is my playground for classical machine learning. I use it to take
algorithms apart, implement them from scratch, and check my understanding
against scikit-learn and other established libraries.

Most topics live in a separate Jupyter notebook. A typical notebook goes from
the idea and implementation to a small experiment where the custom model and a
library baseline train on the same data. The goal is not to beat scikit-learn;
it is to understand why an algorithm works and catch mistakes that a nice-looking
plot might hide.

## 📚 What's inside

- decision trees for classification and regression;
- bagging, random forests, gradient boosting, and stacking;
- linear and logistic regression trained with SGD;
- k-nearest neighbours and neighbour-search indexes: k-d tree, Annoy-style
  random projection trees, LSH, and HNSW;
- grid search and random search;
- notebooks about metrics, Matplotlib, and Optuna;
- solutions for the Titanic and Spaceship Titanic Kaggle competitions.

There are also shared plotting and evaluation helpers in `src/`, plus starter
notebooks in `templates/`.

## 📊 A few results

The table below gives a quick idea of how the custom implementations compare
with library versions. The values come from saved notebook outputs and use a
held-out 20% test split.

| Algorithm | Task | Custom | Library |
| --- | --- | ---: | ---: |
| [Decision tree](learning/algorithms/decision_trees/decision_tree_classification.ipynb) | Classification, accuracy | 1.000000 | 1.000000 |
| [Random forest](learning/algorithms/ensemble_methods/random_forest/random_forest_classification.ipynb) | Classification, accuracy | 1.000000 | 1.000000 |
| [Logistic regression](learning/algorithms/regression_algorithms/logistic_regression.ipynb) | Classification, accuracy | 0.850000 | 0.850000 |
| [kNN](learning/algorithms/knn/knn_classification.ipynb) | Classification, accuracy | 0.970000 | 0.965000 |
| [Decision tree](learning/algorithms/decision_trees/decision_tree_regression.ipynb) | Regression, R² | 0.909980 | 0.909980 |
| [Linear regression](learning/algorithms/regression_algorithms/linear_regression.ipynb) | Regression, R² | 0.937336 | 0.937415 |
| [Gradient boosting](learning/algorithms/ensemble_methods/gradient_boosting/gradient_boosting_tree_regression.ipynb) | Regression, R² | 0.907815 | 0.907815 |

These are small synthetic datasets, so the scores are sanity checks rather than
benchmarks. The interesting part is inside the notebooks: fitted parameters,
metric tables, decision boundaries, and the cases where the implementations do
not quite agree.

The neighbour-search notebooks currently compare classification accuracy only.
They do not benchmark query time, build time, memory use, or index recall, so no
performance claims are made for the approximate indexes.

## 🏆 Kaggle experiments

The most complete competition notebook is
[Spaceship Titanic](competitions/spaceship_titanic/spaceship_titanic.ipynb). It
includes feature engineering, a comparison of several models, and CatBoost
tuning with Optuna.

| Metric | Score |
| --- | ---: |
| Cross-validation accuracy | 0.815986 |
| Hold-out accuracy | 0.812536 |
| Hold-out F1 | 0.816234 |
| Hold-out ROC AUC | 0.899520 |
| Kaggle public leaderboard | 0.80500 |

Competition datasets are not stored in the repository. Download them from
Kaggle and place the CSV files in the corresponding `competitions/*/data/`
directory before running a competition notebook.

## 🚀 Getting started

You will need Python 3.13+, [uv](https://docs.astral.sh/uv/), and optionally
[Task](https://taskfile.dev/).

```sh
git clone https://github.com/NKTKLN/classical-ml-lab.git
cd classical-ml-lab
task init
uv run jupyter lab
```

If you do not use Task, replace `task init` with:

```sh
uv sync --all-groups
uv run pre-commit install --install-hooks
```

Notebooks under `learning/` generate their own data and can be run immediately.
Only the competition notebooks require separately downloaded datasets.

## 🛠️ Useful commands

| Command | What it does |
| --- | --- |
| `task init` | Installs dependencies and Git hooks |
| `task sync` | Synchronizes all dependency groups |
| `task fmt` | Formats code and applies safe Ruff fixes |
| `task lint` | Runs Ruff, the formatting check, and mypy |
| `task audit` | Checks dependencies for known vulnerabilities |
| `task precommit-run` | Runs all pre-commit hooks |

Run `task --list` to see the full list.

## 📁 Project structure

```text
.
├── learning/       # Algorithms, metrics, and library notes
├── competitions/   # Kaggle experiments
├── src/            # Shared evaluation and plotting helpers
├── templates/      # Starter notebooks
├── pyproject.toml  # Dependencies and tool configuration
└── Taskfile.yml    # Common development commands
```

## 📜 License

This project is available under the [MIT License](./LICENSE.md).
