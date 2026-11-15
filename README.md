<h1 align="center">Роман Ларионов</h1>

<p align="center">
  <b>Applied Machine Learning & Data Analysis</b><br>
  Студент физфака МГУ · ML-исследователь в НИИЯФ МГУ · ищу стажировку в ML / Data Science
</p>

<p align="center">
  <a href="https://t.me/larionovN1"><img src="https://img.shields.io/badge/Telegram-@larionovN1-26A5E4?logo=telegram&logoColor=white" alt="Telegram"></a>
  <a href="mailto:2005roma.roman@mail.ru"><img src="https://img.shields.io/badge/Почта-2005roma.roman@mail.ru-005FF9?logo=maildotru&logoColor=white" alt="Почта"></a>
  <a href="https://doi.org/10.1134/S1054661826700896"><img src="https://img.shields.io/badge/Статья-PRIA_2026-1f6feb?logo=doi&logoColor=white" alt="Статья"></a>
  <img src="https://img.shields.io/badge/Москва-555?logo=googlemaps&logoColor=white" alt="Москва">
</p>

## Коротко

- **Ускорил свой алгоритм отбора признаков в 170–870 раз**: точный аналитический пересчёт ошибки вместо переобучения
  моделей — отбор из 5 427 признаков за 194 секунды вместо 9–47 часов, результат совпадает с исходным до 10⁻¹⁴.
- **Первый автор статьи** в *Pattern Recognition and Image Analysis* (2026) и доклада на PRIP’2025 — об отборе
  мультиколлинеарных признаков в обратных задачах геофизики.
- **Полноволновая инверсия сейсмограмм**: честно сравнил 7 подходов, от PINN и диффузионных моделей до классической
  FWI, и построил своё GPU-ядро FWI на OpenCL — в 4 раза быстрее Deepwave.
- **Рекомендации и ранжирование**: RL-дообучение генеративного рекомендера, автоматизация признаков на Yambda-50M,
  пет-проекты по скорингу, поиску, рекомендациям и MLOps.
- Подход к экспериментам: сильный бейзлайн, разбиение без утечек, контрольные расчёты и абляции. Если метод не
  сработал — разбираюсь почему и фиксирую вывод.

## Опыт

### НИИЯФ МГУ · ML-инженер, исследователь · ноябрь 2024 — сейчас
Лаборатория адаптивных методов обработки данных. Отбор входных признаков для нейросетевого решения обратных задач:
магнитотеллурическое зондирование (до 30 000 примеров, 2 418 мультиколлинеарных признаков) и фотолюминесцентная
спектроскопия углеродных точек — определение концентраций ионов металлов в воде (5 427 спектральных каналов).

- Сравнил три класса методов отбора — filter, embedded (важности бустинга, анализ весов нейросети) и wrapper —
  под MLP, градиентный бустинг и линейную регрессию. Сократил вход до 750 признаков (30%) без статистически значимой
  потери качества; результаты опубликованы.
- Разработал пакетный обратный отбор **BSBS** и его **ускоренную версию**: модель без каждого признака выражается через
  одну обратную матрицу гребневой регрессии, ошибки всех кандидатов итерации — за одно обращение матрицы с
  кросс-валидацией. 194 с вместо ≈ 9,2 ч и ≈ 47 ч; расширения — ускоренный RFE, отбор группами каналов, двойственная
  форма для случая «признаков больше, чем примеров».
- Скорость позволила сравнить десятки вариантов предобработки: 144 и 120 полных отборов за несколько часов вместо
  десятков суток, сетки нормировок из 324 и 246 заданий на сервере лаборатории. Например, отбор по нормированным
  спектрам даёт качество всего спектра уже на 100 каналах из 5 427.
- Провёл ревизию собственного кода: нашёл ошибку направления в старой реализации отбора и смещение из-за подгонки под
  фиксированные разбиения кросс-валидации, проверил побитовую воспроизводимость. Около 150 автотестов: каждая быстрая
  формула сверяется с честным переобучением.

→ [Geo_Features_GIT](https://github.com/Killvarus/Geo_Features_GIT)

### EnergyCraft · ML-инженер, разработчик, исследователь · март 2026 — сейчас
Восстановление скоростной модели среды Vp(x, z) по сейсмограммам SEG-Y; цель — программа уровня открытого IFOS2D.
Все расчёты вслепую: истинная модель используется только для итоговой оценки, как с полевыми данными.

- **Поиск метода (март — сентябрь):** сравнил 7 подходов — PINN, диффузионную модель, частотную постановку,
  InversionNet / OpenFWI (не переносится на чужую геометрию: R² −2,8 без дообучения), Implicit FWI, классическую FWI,
  томографию первых вступлений (R² фона 0,345 → 0,395). Вывод: нейросетевые постановки разрез не восстанавливают,
  рабочий путь — классическая FWI.
- **Своё ядро FWI (октябрь — ноябрь):** GPU-ядра на OpenCL для прямой и сопряжённой задачи, совпадение с Deepwave
  до 7·10⁻⁶ по трассам и 2,6·10⁻⁶ по градиенту, инверсия в 4 раза быстрее (15 мин вместо 61). Конвейер «только из
  данных»: геометрия из заголовков, автопикинг первых вступлений, оценка импульса, многомасштабная инверсия с L-BFGS,
  контроль качества на взрывах вне инверсии.
- **Результаты:** модель с наклонной границей — ошибка скорости 290 → 114 м/с, глубина границы с точностью ~6 м;
  модель zoloto — ошибка 740 → 434 м/с; закон плотности программа выбирает по данным и он совпадает с законом
  генератора.
- Моя роль: постановка задач, выбор метода, генерация данных, проверка результатов, предзащита.

→ [EnergyCraft](https://github.com/Killvarus/EnergyCraft)

## Образование

**МГУ имени М.В. Ломоносова**, физический факультет · специалитет «Фундаментальная и прикладная физика» · 2023–2029<br>
Кафедра математического моделирования и информатики.

## Исследовательские проекты

| проект | о чём | результат |
|---|---|---|
| [**Geo_Features_GIT**](https://github.com/Killvarus/Geo_Features_GIT) | Отбор мультиколлинеарных признаков для обратных задач: магнитотеллурика и спектроскопия | Ускоренный BSBS: в 170–870 раз быстрее при совпадении до 10⁻¹⁴; вход сокращается до 30% без потери качества |
| [**EnergyCraft**](https://github.com/Killvarus/EnergyCraft) | Полноволновая инверсия сейсмограмм: 7 подходов, своё ядро FWI на OpenCL | Ошибка скорости 740 → 434 м/с на zoloto, 290 → 114 м/с на наклонной границе; ядро в 4 раза быстрее Deepwave |
| [**recsys-feature-automation**](https://github.com/Killvarus/recsys-feature-automation) | Можно ли заменить ручные признаки для ранжирования в рекомендациях автоматическим перебором и отбором. Yambda-50M (Яндекс Музыка), 47,8 млн событий | LightGBM на 246 ручных признаках — ROC-AUC 0,909; найдена и устранена утечка, давшая 0,985. 100 автопризнаков после отбора BSBS заменяют все ручные |
| [**kion-rl-recsys**](https://github.com/Killvarus/kion-rl-recsys) | RL-дообучение GPT-2-рекомендера по выученной награде на данных KION | Показан reward hacking: без регуляризации половина пользователей получает один и тот же первый фильм. При поточечной награде RL и переранжирование лежат на одном фронте Парето |

## Пет-проекты

| проект | что внутри | результат |
|---|---|---|
| [**credit-scoring**](https://github.com/Killvarus/credit-scoring) | EDA и проверка гипотез, WoE-скоркарта, KNN, лес, LightGBM / CatBoost / XGBoost, SHAP, экономика порога, симуляция A/B-теста | ROC-AUC 0,784 (+0,050 к логрегрессии), прибыль на заявителя +45%; расчёт мощности A/B |
| [**credit-scoring-service**](https://github.com/Killvarus/credit-scoring-service) | MLOps: FastAPI, Docker, переобучение в Airflow с проверкой данных и champion / challenger, PSI-мониторинг, Prometheus, Telegram-бот, Kubernetes, Spark | 23 теста; в CI — сборка образа, смоук-тест контейнера, валидация манифестов, Spark-джоба |
| [**recsys-movielens**](https://github.com/Killvarus/recsys-movielens) | 12 моделей с нуля: популярное, content-based, ItemKNN, EASE, iALS, BPR, Item2Vec, SASRec, MultVAE, LightGCN и др.; двухэтапная схема с LambdaMART; многорукие бандиты | Двухэтапная схема — NDCG@10 0,101 против 0,080 у EASE; последние 5 фильмов важнее всей истории |
| [**learning-to-rank**](https://github.com/Killvarus/learning-to-rank) | Поиск по каталогу мебели (WANDS): BM25 с нуля, BERT, поточечный / попарный / списочный подходы, DSSM | NDCG@10 0,844 у RankNet против 0,805 у BM25 (p = 2·10⁻⁷) |
| [**naive-bayes-spam**](https://github.com/Killvarus/naive-bayes-spam) | Наивный Байес с нуля на Enron-Spam: абляция предобработки, порог под долю ложных срабатываний, перенос между ящиками | F1 0,987, совпадает со sklearn; FPR 0,5% при recall 0,90 |

У каждого пет-проекта есть `GUIDE.md` — подробный разбор теории, решений и типичных вопросов по теме.

## Публикации и доклады

- **R.A. Larionov**, I.V. Isaev, A.A. Guskov, I.E. Obornev, S.A. Dolenko. *Selection and Analysis of Multicollinear
  Input Features in Solving Inverse Problems of Exploration Geophysics*. Pattern Recognition and Image Analysis, 2026,
  vol. 36, no. 3, pp. 1094–1103. [DOI: 10.1134/S1054661826700896](https://doi.org/10.1134/S1054661826700896)
- 17th International Conference on Pattern Recognition and Information Processing (PRIP’2025), Минск — доклад и
  статья в сборнике: *Application of Algorithms for Selection and Analysis of Multicollinear Input Features in Solving
  Inverse Problems of Exploration Geophysics* (WoS Q3).
- РИНЦ: «Планирование следующего поколения кремниевой фотоники»; «Гидрогели для активной фотоники».

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
![OpenCL](https://img.shields.io/badge/OpenCL-ED1C24)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Airflow](https://img.shields.io/badge/Airflow-017CEE?logo=apacheairflow&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?logo=git&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?logo=linux&logoColor=black)

**Методы:** регрессия, градиентный бустинг, нейросети, PINN, отбор и генерация признаков, PCA / kernel PCA / PLS,
кросс-валидация, интерпретация моделей, ранжирование, рекомендательные системы, A/B-тесты, обратные задачи,
сопряжённая задача, L-BFGS.<br>
**Математика:** линейная алгебра, матанализ, теория вероятностей и матстатистика, дифференциальные уравнения, методы
оптимизации.<br>
**Английский:** B1 — чтение и написание научных статей, доклады на международных конференциях.

## Другое

[adaptive-logistics](https://github.com/Killvarus/adaptive-logistics) — локальный планировщик смены перевозчика:
сервер пересчитывает экономику рейсов при смене цен и собирает заказы в цепочки (FastAPI, OR-Tools CP-SAT, React).
Данные синтетические.

## Контакты

Telegram [@larionovN1](https://t.me/larionovN1) · почта ananev.ro23@physics.msu.ru, 2005roma.roman@mail.ru ·
VK [iamlarionov1](https://vk.com/iamlarionov1)
