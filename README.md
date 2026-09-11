# 🧪 Classical ML Lab

[![Python](https://img.shields.io/badge/Python-3.13%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-notebooks-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-baseline-F7931E?logo=scikitlearn&logoColor=white)](https://scikit-learn.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-baseline-337AB7)](https://xgboost.readthedocs.io/)
[![CatBoost](https://img.shields.io/badge/CatBoost-FFCC00)](https://catboost.ai/)
[![uv](https://img.shields.io/badge/uv-managed-DE5FE9?logo=uv&logoColor=white)](https://docs.astral.sh/uv/)
[![Ruff](https://img.shields.io/badge/linting-ruff-D7FF64?logo=ruff&logoColor=black)](https://docs.astral.sh/ruff/)
[![Checked with mypy](https://img.shields.io/badge/mypy-checked-2A6DB2.svg)](https://mypy-lang.org/)
[![Task](https://img.shields.io/badge/Task-29BEB0?logo=task&logoColor=white)](https://taskfile.dev/)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-FAB040?logo=pre-commit&logoColor=black)](https://pre-commit.com/)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-FE5196?logo=conventionalcommits&logoColor=white)](https://www.conventionalcommits.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE.md)

**Classical ML Lab** is a study repository where each classical algorithm is
written from scratch in its own notebook — decision trees, bagging, random
forests, gradient boosting, stacking, SGD linear and logistic regression, kNN
and four nearest-neighbour indexes — and then fitted side by side with the
scikit-learn or XGBoost implementation of the same algorithm, on the same split,
with the same hyperparameters and the same seed.

The comparison is the whole design. Writing an algorithm yourself is how you
learn its mechanics: where the split criterion is actually evaluated, what the
residual in boosting really is, why an HNSW layer needs an entry point. But a
hand-written model that merely runs proves nothing — it can be subtly wrong and
still draw a plausible decision boundary. So every notebook ends with one table
in which the custom model and the industrial one are scored against each other.
Agreement with a library that thousands of people rely on is the correctness
check this repository has in place of a test suite, and where the two disagree
the gap is reported rather than tuned away.

Every number below is copied from a stored cell output in the notebook each row
links to. Nothing here is estimated or re-run from memory.

## 📊 Custom implementation vs. library

Classification, **accuracy** on the held-out 20% of
`train_test_split(test_size=0.2, random_state=42)`:

| Algorithm | Notebook dataset | Custom | Library baseline | Δ |
| --- | --- | --- | --- | --- |
| [Decision tree](learning/algorithms/decision_trees/decision_tree_classification.ipynb) | `make_circles`, 300×2 | 1.000000 | `DecisionTreeClassifier` 1.000000 | 0.000000 |
| [Bagging](learning/algorithms/ensemble_methods/bagging/bagging_tree_classification.ipynb) | `make_circles`, 300×2 | 1.000000 | `BaggingClassifier` 1.000000 | 0.000000 |
| [Random forest](learning/algorithms/ensemble_methods/random_forest/random_forest_classification.ipynb) | `make_circles`, 300×2 | 1.000000 | `RandomForestClassifier` 1.000000 | 0.000000 |
| [Gradient boosting](learning/algorithms/ensemble_methods/gradient_boosting/gradient_boosting_tree_classification.ipynb) | `make_circles`, 300×2 | 1.000000 | `GradientBoostingClassifier` 1.000000 | 0.000000 |
| [Gradient boosting](learning/algorithms/ensemble_methods/gradient_boosting/gradient_boosting_tree_classification.ipynb) | `make_circles`, 300×2 | 1.000000 | `XGBClassifier` 0.983333 | +0.016667 |
| [Stacking](learning/algorithms/ensemble_methods/stacking/stacking_classification.ipynb) | `make_classification`, 1000×5 | 0.850000 | `StackingClassifier` 0.850000 | 0.000000 |
| [Logistic regression (SGD)](learning/algorithms/regression_algorithms/logistic_regression.ipynb) | `make_classification`, 100×5 | 0.850000 | `LogisticRegression` 0.850000 | 0.000000 |
| [kNN (brute force)](learning/algorithms/knn/knn_classification.ipynb) | `make_classification`, 1000×2, 4 classes | 0.970000 | `KNeighborsClassifier` 0.965000 | +0.005000 |
| [Grid search CV](learning/algorithms/hyperparameter_tuning/grid_search.ipynb) | `load_iris` | 1.000000 | `GridSearchCV` 1.000000 | 0.000000 |
| [Random search CV](learning/algorithms/hyperparameter_tuning/random_search.ipynb) | `load_iris` | 1.000000 | `RandomizedSearchCV` 1.000000 | 0.000000 |

Regression, **R²** on the held-out 20%. Every row uses the same dataset,
`make_regression(n_samples=100, n_features=1, noise=10, bias=37.0,
random_state=42)`:

| Algorithm | Custom | Library baseline | Δ |
| --- | --- | --- | --- |
| [Decision tree](learning/algorithms/decision_trees/decision_tree_regression.ipynb) | 0.909980 | `DecisionTreeRegressor` 0.909980 | 0.000000 |
| [Gradient boosting](learning/algorithms/ensemble_methods/gradient_boosting/gradient_boosting_tree_regression.ipynb) | 0.907815 | `GradientBoostingRegressor` 0.907815 | 0.000000 |
| [kNN](learning/algorithms/knn/knn_regression.ipynb) | 0.935034 | `KNeighborsRegressor` 0.935049 | −0.000015 |
| [Linear regression (SGD)](learning/algorithms/regression_algorithms/linear_regression.ipynb) | 0.937336 | `LinearRegression` 0.937415 | −0.000079 |
| [Stacking](learning/algorithms/ensemble_methods/stacking/stacking_regression.ipynb) | 0.926464 | `StackingRegressor` 0.921659 | +0.004805 |
| [Bagging](learning/algorithms/ensemble_methods/bagging/bagging_tree_regression.ipynb) | 0.932420 | `BaggingRegressor` 0.917487 | +0.014933 |
| [Random forest](learning/algorithms/ensemble_methods/random_forest/random_forest_regression.ipynb) | 0.932420 | `RandomForestRegressor` 0.917487 | +0.014933 |

What the rows are worth varies, and the differences are the interesting part:

* **The two regression rules converge on the same parameters, not just the same
  score.** The SGD linear and logistic notebooks print the fitted coefficients
  next to scikit-learn's, and they match at full printed precision —
  `44.244182155974194` with intercept `37.089619` for linear regression, and an
  identical coefficient vector for logistic regression. Reaching the analytic
  least-squares solution by gradient descent is a far stronger correctness signal
  than any accuracy row, and the leftover 0.000079 R² is a difference too small
  to survive the six decimals the parameter table displays.
* **The tree rows that agree, agree completely.** Decision tree and gradient
  boosting regression match scikit-learn on MAE, MSE and R² to every printed
  digit, which is a stronger statement than the accuracy column can make.
* **The 1.000000 classification rows prove less than they look like.** Those are
  a 60-sample test split of two well-separated concentric circles: both
  implementations hit the ceiling, so the agreement is real but weakly informative.
  The `make_classification` rows (1000 and 100 samples) are the ones that
  discriminate.
* **The +0.015 R² on bagging and random forest is the largest gap in either
  table**, and both ensembles come out ahead of scikit-learn. On a 20-sample test
  split that is well inside the spread produced by drawing different bootstrap
  samples; it is not evidence that the custom ensemble is better.
* **Bagging and random forest report identical figures** because the dataset has
  a single feature. With `max_features` left at its default, a random forest on
  one feature has nothing to subsample and degenerates into bagging, so the two
  notebooks fit the same ensemble.
* **Both search notebooks select the same hyperparameters** as scikit-learn
  (`C=10`, `kernel=rbf`, `gamma=scale`) at the same best CV accuracy, 0.966667.

## 🔍 Nearest-neighbour indexes

Four index structures are implemented from scratch and scored against
scikit-learn's exact `KNeighborsClassifier` on `make_classification` data with 2
features and 4 classes. Dataset size grows with the index, so the rows are not
comparable to each other — only each row to its own baseline:

| Index | Dataset | Custom accuracy | Exact baseline | Δ |
| --- | --- | --- | --- | --- |
| [k-d tree](learning/algorithms/knn/knn_classification_with_k-d_trees.ipynb) | 1 000 points | 0.970000 | 0.965000 | +0.005000 |
| [Annoy-style random projection forest](learning/algorithms/knn/annoy_classification.ipynb) | 1 000 points | 0.975000 | 0.965000 | +0.010000 |
| [LSH](learning/algorithms/knn/knn_classification_with_lsh.ipynb) | 5 000 points | 0.982000 | 0.981000 | +0.001000 |
| [HNSW](learning/algorithms/knn/knn_classification_with_hnsw.ipynb) | 10 000 points | 0.949500 | 0.985000 | −0.035500 |

> [!IMPORTANT]
> **Accuracy is the only thing measured here.** None of these notebooks times a
> build or a query, and none measures index size — there is no `%%timeit`, no
> `perf_counter` and no allocation tracking anywhere in the repository. The speed
> and memory trade-off that is the entire reason to use an approximate index is
> not quantified, so it is not claimed.

The Δ column is also not index recall. The custom classifier is not a drop-in
replacement for the baseline: it uses Minkowski distance with `p=5` and Gaussian
kernel weighting (`h=5.8`), while `KNeighborsClassifier` runs Euclidean distance
with uniform weights. An approximate index can at best match exact search under
the same metric, so the small positive differences must come from that weighting
scheme rather than from the index itself.

Two rows read as correctness checks rather than trade-offs. The k-d tree is an
exact structure, and it returns 0.970000 — the same figure the brute-force
custom kNN produces on the same 1 000-point dataset, which is what a correct
exact index has to do. HNSW's −0.0355 is the one difference large enough to read
as an index genuinely dropping neighbours, and it shows up on the largest of the
four datasets, where an approximate structure is under the most pressure.

## 🏆 Competitions

**[Spaceship Titanic](https://www.kaggle.com/competitions/spaceship-titanic)** —
8 693 training rows expanded to 32 engineered features (passenger-group size and
family links, cabin deck/number/side, total and per-group spend, and an explicit
missing-value indicator for every column that has one), then a CatBoost
classifier tuned by Optuna over 150 trials.

| Measurement | Value |
| --- | --- |
| Best cross-validated accuracy (Optuna) | 0.815986 |
| Hold-out accuracy | 0.812536 |
| Hold-out F1 | 0.816234 |
| Hold-out ROC AUC | 0.899520 |
| Kaggle public leaderboard | 0.80500 |

The leaderboard figure is the only number in this README that does not come from
a cell output — the notebook does not store one — and is taken from the commit
that produced the submission (`b409744`). Before tuning, the same hold-out split
ranks the candidates CatBoost 0.805635, LightGBM 0.793560, random forest
0.793560, XGBoost 0.787234, kNN 0.747556, which is why CatBoost is the one that
gets tuned.

Competition data is **not** in the repository — `.gitignore` keeps
`competitions/*/data/*` out. Download the CSVs from Kaggle into the matching
`data/` folder before running a competition notebook.

## 📦 Dependencies

* [Python 3.13+](https://www.python.org/downloads/) — the floor in `pyproject.toml`
* [uv](https://docs.astral.sh/uv/) — environment and dependency management
* [Task](https://taskfile.dev/) — task runner; optional, every task is a short
  `uv run` command you can type by hand
* [Jupyter](https://jupyter.org/) — running the notebooks

Python packages are split into [dependency
groups](https://docs.astral.sh/uv/concepts/projects/dependencies/#dependency-groups)
in `pyproject.toml`. All of them install on a bare `uv sync`, because a notebook
generally needs the full stack:

| Group | Purpose |
| --- | --- |
| `data` | numpy, pandas |
| `ml` | scikit-learn, XGBoost, CatBoost, LightGBM — the baselines everything is compared against |
| `viz` | matplotlib, seaborn, plotly |
| `tuning` | optuna, hyperopt, scikit-optimize |
| `notebook` | ipywidgets, tqdm, colorama and other notebook UX helpers |
| `dev` | ruff, mypy, pre-commit, commitizen, pip-audit, deptry |

## 🚀 Getting Started

Clone the repository:

```sh
git clone https://github.com/NKTKLN/classical-ml-lab.git
cd classical-ml-lab
```

Install dependencies and the git hooks:

```sh
task init
```

Without [Task](https://taskfile.dev/), the same two steps directly:

```sh
uv sync --all-groups
uv run pre-commit install --install-hooks
```

Then launch Jupyter and open any notebook:

```sh
uv run jupyter lab
```

Every notebook under `learning/` builds its own data — a synthetic generator or
a dataset bundled with scikit-learn — so it runs end to end straight after a
clone, and re-running one reproduces the numbers in the tables above. Only the
`competitions/` notebooks need files you have to fetch from Kaggle first.

## 🛠️ Common Tasks

`task --list` shows everything. The ones worth knowing:

| Command | Description |
| --- | --- |
| `task init` | Full setup: sync dependencies, install hooks |
| `task sync` | `uv sync --all-groups` |
| `task sync-frozen` | Same, but pinned to `uv.lock` |
| `task fmt` | `ruff format` then `ruff check --fix` |
| `task lint` | Ruff, format check and mypy |
| `task typecheck` | mypy over `src` |
| `task audit` | `pip-audit` over the dependency tree |
| `task unused-libs` | `deptry` — declared dependencies nothing imports |
| `task precommit-run` | Run every hook against all files |
| `task cz-commit` | Commit through commitizen |

The pre-commit hooks run ruff and `ruff format` on everything, including
notebooks (`extend-include = ["*.ipynb"]` in the ruff config), plus gitleaks,
`uv lock` consistency, and commitizen on the commit message. mypy is not one of
the hooks, and `task typecheck` does not currently come back clean: it reports 24
errors, all of them `import-untyped` or `no-any-unimported` raised because
scikit-learn, seaborn and the rest of the ML stack ship no type stubs. None come
from the code in `src/`, which is fully annotated.

There are no tests in this repository, and `task check` refers to `test-cov` and
`build` targets that `Taskfile.yml` does not define, so that one task fails.
Correctness here is argued by the comparison tables above, not by a suite.

## 📁 Source layout

```text
.
├── learning/
│   ├── algorithms/                 # One notebook per algorithm: implementation, then comparison
│   │   ├── decision_trees/         # Classification and regression trees
│   │   ├── knn/                    # Brute force, k-d trees, Annoy-style, LSH, HNSW
│   │   ├── regression_algorithms/  # SGD linear and logistic regression
│   │   ├── ensemble_methods/       # Bagging, random forest, gradient boosting, stacking
│   │   └── hyperparameter_tuning/  # Grid search CV, random search CV
│   ├── metrics/                    # Metric behaviour under imbalance, outliers, edge cases
│   └── libraries/                  # Tooling notebooks (matplotlib, optuna)
├── competitions/                   # Kaggle solutions; each has a gitignored data/ folder
├── src/
│   ├── evaluations/                # The metric tables the comparisons are printed from
│   └── plots/                      # Confusion matrices, ROC/PR curves, decision boundaries
├── templates/                      # Starter notebooks (algorithm.ipynb, competition.ipynb)
├── pyproject.toml                  # Dependency groups, ruff, mypy, commitizen config
└── Taskfile.yml                    # Developer commands
```

The comparison tables in every notebook are rendered by the same helpers in
`src/evaluations/`, which is why a metric means the same thing across all of
them.

## 📜 License

This project is licensed under the MIT License. See the [LICENSE.md](./LICENSE.md)
file for details.
