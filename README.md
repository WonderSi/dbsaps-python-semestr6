# Лабораторная работа 11. PySpark — Классификация

## Что делает ноутбук

Решаются две задачи классификации с помощью **PySpark ML** — без pandas и без sklearn.

---

## Файлы

| Файл | Описание |
|------|----------|
| `lab11_spark.ipynb` | Основной ноутбук с решением |
| `iris.csv` | Датасет ирисов (150 записей, 3 класса) |
| `titanic.csv` | Датасет Титаника (891 запись, 2 класса) |

---

## Часть 1 — Iris

**Задача:** по 4 числовым признакам цветка определить его вид (Setosa / Versicolor / Virginica).

**Пайплайн:**
```
StringIndexer → VectorAssembler → LogisticRegression
```

| Шаг | Что происходит |
|-----|----------------|
| `StringIndexer` | Переводит строку `variety` в число: Setosa→0, Versicolor→1, Virginica→2 |
| `VectorAssembler` | Собирает 4 числовых столбца в один вектор `features` |
| `LogisticRegression` | Обучает мультиклассовый классификатор |

**Оценка:** `MulticlassClassificationEvaluator` (accuracy) + матрица ошибок.

---

## Часть 2 — Titanic

**Задача:** по признакам пассажира предсказать выжил он или нет (бинарная классификация).

**Признаки:** `Pclass`, `Sex`, `Age`, `SibSp`, `Parch`, `Fare`, `Embarked`

**Пайплайн:**
```
StringIndexer → OneHotEncoder → VectorAssembler → LogisticRegression
```

| Шаг | Что происходит |
|-----|----------------|
| `StringIndexer` | Кодирует `Sex` и `Embarked` в числа |
| `OneHotEncoder` | Убирает ложную упорядоченность: male/female — не «больше» и «меньше» |
| `VectorAssembler` | Собирает все признаки в вектор `features` |
| `LogisticRegression` | Обучает бинарный классификатор |

**Оценка:** `MulticlassClassificationEvaluator` (accuracy) + `BinaryClassificationEvaluator` (AUC-ROC) + матрица ошибок.

---

## Запуск

1. Убедись что установлен Java (JDK 21) и PySpark
2. Положи `iris.csv` и `titanic.csv` в папку с ноутбуком
3. Запускай ячейки по порядку сверху вниз
