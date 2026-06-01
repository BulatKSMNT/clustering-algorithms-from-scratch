# Unsupervised Learning: Clustering & Feature Engineering 

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![NumPy](https://img.shields.io/badge/Math-NumPy-013243.svg?logo=numpy)
![Scikit-Learn](https://img.shields.io/badge/ML-Scikit--Learn-F7931E.svg?logo=scikit-learn)
![Machine Learning](https://img.shields.io/badge/ML-Unsupervised-success.svg)

## О проекте (About the Project)
Этот репозиторий посвящен алгоритмам кластеризации (сегментации данных) и их практическому применению. Главная фишка проекта — это не просто группировка данных ради визуализации, а **создание гибридного ML-пайплайна**, где результаты работы моделей без учителя (Unsupervised) используются для улучшения качества моделей с учителем (Supervised).

В рамках бизнес-задачи по предсказанию стоимости аренды недвижимости, алгоритмы кластеризации применяются к геолокационным данным (широта и долгота), чтобы автоматически выявить "престижные" и "дешевые" районы, создав из них новые мощные предикторы для модели Lasso Regression.

---

## Технологический стек
* **Math & Core:** `numpy`, `pandas`
* **Machine Learning:** Custom K-Means & DBSCAN, `scikit-learn` (GMM, Agglomerative Clustering, Lasso)
* **Metrics & Evaluation:** Silhouette Score, Distortion (Elbow Method)
* **Visualization:** `matplotlib`, `seaborn`

---

## Ключевые этапы и достижения (Key Highlights)

### 1. Clustering Algorithms "Under the Hood" (Алгоритмы с нуля)
Вместо стандартных импортов, базовые алгоритмы написаны с использованием чистой математики на NumPy:
* **K-Means:** Реализован итеративный процесс вычисления центроидов и переназначения кластеров (Update & Assignment steps).
* **DBSCAN:** Реализован алгоритм пространственной кластеризации на основе плотности (с параметрами `eps` и `min_samples`), отлично справляющийся с выбросами (шумом) и кластерами сложной формы.

### 2. Продвинутая кластеризация (Advanced Segmentation)
Помимо базовых методов, в проекте исследованы и применены:
* **Agglomerative Clustering:** Иерархический подход (bottom-up) для построения дендрограмм.
* **Gaussian Mixture Models (GMM):** Вероятностный подход к кластеризации с использованием EM-алгоритма (Expectation-Maximization) для работы с пересекающимися распределениями.

### 3. Оценка качества кластеров (Evaluation)
Для выбора оптимального количества кластеров ($K$) и настройки гиперпараметров реализован математический расчет метрик:
* **Elbow Method (Метод локтя):** Расчет функции искажения (Distortion / Inertia).
* **Silhouette Coefficient:** Оценка плотности и изолированности кластеров (внутрикластерное vs. межкластерное расстояние).

### 4. Unsupervised for Feature Engineering (Гибридный пайплайн)
* Проведена пространственная кластеризация координат объектов недвижимости (`longitude`, `latitude`).
* Полученные метки кластеров были закодированы и добавлены в качестве **новых признаков** в обучающую выборку.
* Итоговая модель **Lasso Regression** обучена на расширенном датасете. Анализ весов модели (Feature Importance) доказал высокую значимость сгенерированных пространственных кластеров для предсказания цены аренды.
