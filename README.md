<h1 align="center">Роман Ларионов</h1>

<p align="center">
  Студент физического факультета МГУ · ML-исследователь в НИИЯФ МГУ · ищу стажировку в ML / Data Science
</p>

<p align="center">
  <a href="https://t.me/larionovN1"><img src="https://img.shields.io/badge/Telegram-@larionovN1-26A5E4?logo=telegram&logoColor=white" alt="Telegram"></a>
  <a href="mailto:2005roma.roman@mail.ru"><img src="https://img.shields.io/badge/Почта-2005roma.roman@mail.ru-005FF9?logo=maildotru&logoColor=white" alt="Почта"></a>
  <a href="https://doi.org/10.1134/S1054661826700896"><img src="https://img.shields.io/badge/Статья-PRIA_2026-1f6feb?logo=doi&logoColor=white" alt="Статья"></a>
  <img src="https://img.shields.io/badge/Москва-555?logo=googlemaps&logoColor=white" alt="Москва">
</p>

## Коротко

- **Исследую ML с 2024 года**: отбор признаков и обратные задачи геофизики в НИИЯФ МГУ, восстановление скоростного
  разреза по сейсмограммам в Energy Craft.
- **Первый автор статьи** в *Pattern Recognition and Image Analysis* (2026) — об отборе мультиколлинеарных признаков.
- **Рекомендательные системы**: RL-дообучение генеративного рекомендера, автоматизация признаков для ранжирования,
  ранжирование и рекомендации на табличных и текстовых данных.
- Подход к экспериментам: сильный бейзлайн, разбиение без утечек, доверительные интервалы и абляции. Если метод
  не сработал — разбираюсь почему и пишу об этом.

## Опыт

**НИИЯФ МГУ** · с октября 2024<br>
Обратная задача магнитотеллурического зондирования. Сравниваю фильтры, встроенный отбор и обёртки, в том числе BSBS,
а также PCA, kernel PCA, PLS и вейвлеты. Вход удаётся сокращать примерно на 70% без заметной потери качества на глубоких
слоях. → [Geo_Features_GIT](https://github.com/Killvarus/Geo_Features_GIT)

**Energy Craft** · с февраля 2026<br>
Полноволновая инверсия лабораторных сейсмограмм SEG-Y. Сравнивал PINN, Implicit FWI и классическую FWI; истинная модель
в обучение не входит. На согласованной съёмке классическая FWI подняла R² крупномасштабного фона с 0,345 до 0,395.
→ [EnergyCraft](https://github.com/Killvarus/EnergyCraft)

## Исследовательские проекты

| проект | о чём | результат |
|---|---|---|
| [**recsys-feature-automation**](https://github.com/Killvarus/recsys-feature-automation) | Можно ли заменить ручные признаки для ранжирования в рекомендациях автоматическим перебором и отбором. Yambda-50M (Яндекс Музыка), 47,8 млн событий | LightGBM на 246 ручных признаках — ROC-AUC 0,909; найдена и устранена утечка, давшая 0,985. 100 автопризнаков после отбора BSBS заменяют все ручные |
| [**kion-rl-recsys**](https://github.com/Killvarus/kion-rl-recsys) | RL-дообучение GPT-2-рекомендера по выученной награде на данных KION: доля досмотра, вовлечённость, возврат пользователя | Показан reward hacking: без регуляризации половина пользователей получает один и тот же первый фильм. При поточечной награде RL и переранжирование по log π + λ·r лежат на одном фронте Парето |
| [**Geo_Features_GIT**](https://github.com/Killvarus/Geo_Features_GIT) | Отбор мультиколлинеарных признаков в обратной задаче магнитотеллурики | Вход сокращается на ~70% без заметной потери качества на глубоких слоях |
| [**EnergyCraft**](https://github.com/Killvarus/EnergyCraft) | Полноволновая инверсия сейсмограмм: PINN, Implicit FWI, классическая FWI | R² фона 0,345 → 0,395 |

## Пет-проекты

| проект | что внутри | результат |
|---|---|---|
| [**credit-scoring**](https://github.com/Killvarus/credit-scoring) | EDA и проверка гипотез, WoE-скоркарта, KNN, лес, LightGBM / CatBoost / XGBoost, SHAP, экономика порога, симуляция A/B-теста | ROC-AUC 0,784 (+0,050 к логрегрессии), прибыль на заявителя +45%; расчёт мощности A/B |
| [**credit-scoring-service**](https://github.com/Killvarus/credit-scoring-service) | MLOps: FastAPI, Docker, переобучение в Airflow с проверкой данных и champion / challenger, PSI-мониторинг, Prometheus, Telegram-бот, Kubernetes, Spark | 23 теста; в CI — сборка образа, смоук-тест контейнера, валидация манифестов, Spark-джоба |
| [**learning-to-rank**](https://github.com/Killvarus/learning-to-rank) | Поиск по каталогу мебели (WANDS): BM25 с нуля, BERT, поточечный / попарный / списочный подходы, DSSM | NDCG@10 0,844 у RankNet против 0,805 у BM25 (p = 2·10⁻⁷) |
| [**naive-bayes-spam**](https://github.com/Killvarus/naive-bayes-spam) | Наивный Байес с нуля на Enron-Spam: абляция предобработки, порог под долю ложных срабатываний, перенос между ящиками | F1 0,987, совпадает со sklearn; FPR 0,5% при recall 0,90 |

У каждого пет-проекта есть `GUIDE.md` — подробный разбор теории, решений и типичных вопросов по теме.

## Публикация

Первый автор: *Application of Algorithms for Selection and Analysis of Multicollinear Input Features in Solving
Inverse Problems of Exploration Geophysics*. Pattern Recognition and Image Analysis, 2026, т. 36, № 3, с. 1094–1103.
Спецвыпуск по конференции PRIP’2025. [DOI: 10.1134/S1054661826700896](https://doi.org/10.1134/S1054661826700896)

## Стек

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?logo=pytorch&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?logo=scikitlearn&logoColor=white)
![LightGBM](https://img.shields.io/badge/LightGBM-2E7D32)
![CatBoost](https://img.shields.io/badge/CatBoost-FFCC00?logoColor=black)
![XGBoost](https://img.shields.io/badge/XGBoost-337AB7)
![Transformers](https://img.shields.io/badge/Hugging_Face-FFD21E?logo=huggingface&logoColor=black)
![pandas](https://img.shields.io/badge/pandas-150458?logo=pandas&logoColor=white)
![Polars](https://img.shields.io/badge/Polars-CD792C?logo=polars&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?logo=numpy&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?logo=scipy&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Airflow](https://img.shields.io/badge/Airflow-017CEE?logo=apacheairflow&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?logo=git&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?logo=linux&logoColor=black)

## Другое

[adaptive-logistics](https://github.com/Killvarus/adaptive-logistics) — локальный планировщик смены перевозчика:
сервер пересчитывает экономику рейсов при смене цен и собирает заказы в цепочки (FastAPI, OR-Tools CP-SAT, React).
Данные синтетические.

## Контакты

Telegram [@larionovN1](https://t.me/larionovN1) · почта ananev.ro23@physics.msu.ru, 2005roma.roman@mail.ru ·
VK [iamlarionov1](https://vk.com/iamlarionov1)
