# Практичне завдання №3 — детекція AI-згенерованих текстів за допомогою FastText і TF-IDF

**Виконав:** Новак Сергій, ФЕІ-43с

Практична робота присвячена порівнянню двох способів побудови векторного представлення тексту:

- Mean Pooling для FastText-векторів;
- TF-IDF Weighted Mean для FastText-векторів.

Для кожного представлення навчаються три класифікатори: SVM з RBF-ядром, Logistic Regression і KNN.

## Дані

Використано датасет [AI vs Human Text Classification Dataset 2026](https://www.kaggle.com/datasets/alitaqishah/ai-vs-human-text-classification-dataset-2026). Він містить тексти двох класів: `human` та `ai`.

CSV-файл уже знаходиться у папці `data`, тому додатково завантажувати датасет не потрібно.

## Структура

- `practice_3_fasttext_tfidf.ipynb` — код, пояснення, графіки та результати роботи;
- `data/ai_vs_human_text_2026.csv` — датасет;
- `requirements.txt` — необхідні Python-пакети.

## Запуск у VS Code

Потрібні Python 3.11 або 3.12 та розширення **Python** і **Jupyter** для VS Code.

```powershell
py -3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m spacy download en_core_web_sm
```

Після встановлення залежностей:

1. Відкрити `practice_3_fasttext_tfidf.ipynb` у VS Code.
2. Вибрати kernel `.venv\Scripts\python.exe`.
3. Натиснути **Run All**.

## Етапи роботи

1. Аналіз структури, балансу класів, довжин текстів і дублікатів.
2. Нормалізація та попередня обробка тексту за допомогою spaCy.
3. Навчання FastText на train-вибірці.
4. Побудова Mean Pooling і TF-IDF Weighted Mean векторів.
5. Навчання SVM, Logistic Regression та KNN.
6. Обчислення F1 macro, Accuracy, Balanced Accuracy і ROC-AUC.
7. Побудова confusion matrices, ROC-кривих і t-SNE-проєкцій.
8. Аналіз геометрії просторів і характерних TF-IDF-маркерів.

## Результати

Після нормалізації та видалення дублікатів залишився 891 унікальний текст. Усі шість комбінацій класифікатора й способу агрегації отримали значення `1.0000` за тестовими метриками.

Такий результат пояснюється сильною шаблонністю датасету та виразними лексичними відмінностями між класами. TF-IDF Weighted Mean трохи покращив геометричні показники простору, але не змінив якість класифікації через уже досягнуту верхню межу метрик.
