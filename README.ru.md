# Classical ML Lab 🧪

[![Python](https://img.shields.io/badge/Python-3.13%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-notebooks-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-baseline-F7931E?logo=scikitlearn&logoColor=white)](https://scikit-learn.org/)
[![uv](https://img.shields.io/badge/uv-managed-DE5FE9?logo=uv&logoColor=white)](https://docs.astral.sh/uv/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE.md)

[English](./README.md) · **Русский**

Это моя учебная лаборатория по классическому машинному обучению. Здесь я
разбираю алгоритмы по частям, пишу их с нуля и сверяю результат с реализациями
из scikit-learn и других известных библиотек.

Почти каждой теме посвящён отдельный Jupyter-ноутбук. Обычно внутри есть
объяснение идеи, собственная реализация и небольшой эксперимент, в котором она
обучается на тех же данных, что и библиотечный аналог. Цель не в том, чтобы
обыграть scikit-learn, а в том, чтобы понять механику алгоритма и вовремя
заметить ошибки, которые легко пропустить за красивым графиком.

## 📚 Что есть в репозитории

- решающие деревья для классификации и регрессии;
- бэггинг, случайный лес, градиентный бустинг и стекинг;
- линейная и логистическая регрессия на SGD;
- метод ближайших соседей и индексы для их поиска: k-d дерево, случайные
  проекции в духе Annoy, LSH и HNSW;
- grid search и random search;
- ноутбуки о метриках, Matplotlib и Optuna;
- решения соревнований Kaggle: Titanic и Spaceship Titanic.

Общие функции для графиков и оценки моделей лежат в `src/`, а в `templates/`
есть заготовки для новых ноутбуков.

## 📊 Несколько результатов

Эта таблица даёт общее представление о том, насколько близки собственные
реализации к библиотечным. Значения взяты из сохранённых выводов ноутбуков;
для проверки использовались отложенные 20% данных.

| Алгоритм | Задача | Своя реализация | Библиотека |
| --- | --- | ---: | ---: |
| [Решающее дерево](learning/algorithms/decision_trees/decision_tree_classification.ipynb) | Классификация, accuracy | 1.000000 | 1.000000 |
| [Случайный лес](learning/algorithms/ensemble_methods/random_forest/random_forest_classification.ipynb) | Классификация, accuracy | 1.000000 | 1.000000 |
| [Логистическая регрессия](learning/algorithms/regression_algorithms/logistic_regression.ipynb) | Классификация, accuracy | 0.850000 | 0.850000 |
| [kNN](learning/algorithms/knn/knn_classification.ipynb) | Классификация, accuracy | 0.970000 | 0.965000 |
| [Решающее дерево](learning/algorithms/decision_trees/decision_tree_regression.ipynb) | Регрессия, R² | 0.909980 | 0.909980 |
| [Линейная регрессия](learning/algorithms/regression_algorithms/linear_regression.ipynb) | Регрессия, R² | 0.937336 | 0.937415 |
| [Градиентный бустинг](learning/algorithms/ensemble_methods/gradient_boosting/gradient_boosting_tree_regression.ipynb) | Регрессия, R² | 0.907815 | 0.907815 |

Датасеты здесь небольшие и в основном синтетические, поэтому эти числа —
проверка здравого смысла, а не полноценный бенчмарк. Самое интересное находится
в ноутбуках: параметры моделей, таблицы метрик, разделяющие границы и случаи,
когда две реализации всё-таки расходятся.

В ноутбуках про поиск соседей пока сравнивается только качество классификации.
Время построения и поиска, расход памяти и recall индекса не измеряются, поэтому
выводов о производительности приближённых индексов здесь нет.

## 🏆 Эксперименты с Kaggle

Самый подробный соревновательный ноутбук —
[Spaceship Titanic](competitions/spaceship_titanic/spaceship_titanic.ipynb). В
нём есть генерация признаков, сравнение нескольких моделей и настройка CatBoost
с помощью Optuna.

| Метрика | Результат |
| --- | ---: |
| Accuracy на кросс-валидации | 0.815986 |
| Accuracy на отложенной выборке | 0.812536 |
| F1 на отложенной выборке | 0.816234 |
| ROC AUC на отложенной выборке | 0.899520 |
| Публичный лидерборд Kaggle | 0.80500 |

Данные соревнований не хранятся в репозитории. Перед запуском скачайте их с
Kaggle и положите CSV-файлы в соответствующую папку
`competitions/*/data/`.

## 🚀 Быстрый старт

Понадобятся Python 3.13+, [uv](https://docs.astral.sh/uv/) и, по желанию,
[Task](https://taskfile.dev/).

```sh
git clone https://github.com/NKTKLN/classical-ml-lab.git
cd classical-ml-lab
task init
uv run jupyter lab
```

Если вы не используете Task, замените `task init` двумя командами:

```sh
uv sync --all-groups
uv run pre-commit install --install-hooks
```

Ноутбуки из `learning/` сами создают данные и готовы к запуску сразу после
установки зависимостей. Отдельно скачивать датасеты нужно только для
соревновательных ноутбуков.

## 🛠️ Полезные команды

| Команда | Что делает |
| --- | --- |
| `task init` | Устанавливает зависимости и Git-хуки |
| `task sync` | Синхронизирует все группы зависимостей |
| `task fmt` | Форматирует код и применяет безопасные исправления Ruff |
| `task lint` | Запускает Ruff, проверку форматирования и mypy |
| `task audit` | Проверяет зависимости на известные уязвимости |
| `task precommit-run` | Запускает все pre-commit-хуки |

Полный список доступен по команде `task --list`.

## 📁 Структура проекта

```text
.
├── learning/       # Алгоритмы, метрики и заметки о библиотеках
├── competitions/   # Эксперименты с Kaggle
├── src/            # Общие функции для оценки и визуализации
├── templates/      # Заготовки ноутбуков
├── pyproject.toml  # Зависимости и настройки инструментов
└── Taskfile.yml    # Основные команды для разработки
```

## 📜 Лицензия

Проект распространяется по лицензии [MIT](./LICENSE.md).
