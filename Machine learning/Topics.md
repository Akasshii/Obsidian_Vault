# ML / DS — карта тем

Карта для самопроверки: пробежаться глазами и понять, где знания актуальны, а где «поплыли».
После `—` перечислено то, что нужно уметь **объяснить своими словами** (как работает, зачем, подводные камни).

**Статусы:**

- `[ ]` — не проходил / не помню
- `[/]` — помню частично, нужно освежить
- `[x]` — уверенно объясню и отвечу на уточняющие вопросы

**Порядок:** данные → классический ML → обучение (loss, оптимизация, регуляризация) → оценка и валидация → unsupervised → deep learning → прикладные области → продакшн.

---

# Часть I. Данные

## 1. EDA и анализ признаков

- [ ] **Типы признаков** — числовые, категориальные (номинальные / порядковые), временные, текстовые; почему от типа зависит обработка
- [ ] **Распределения** — гистограммы, skewness, тяжёлые хвосты; когда это мешает модели
- [ ] **Корреляция Пирсона** — только линейная связь, чувствительна к выбросам
- [ ] **Корреляция Спирмена / Кендалла** — ранговые, ловят монотонную связь
- [ ] **Связь категориальных признаков** — Cramér's V, χ²
- [ ] **Mutual Information** — ловит нелинейные зависимости; минусы (оценка на непрерывных данных)
- [ ] **Корреляция ≠ причинность** — confounders, ложные корреляции
- [ ] **Мультиколлинеарность** — как найти (корреляционная матрица, VIF), чем вредна линейным моделям и почему не вредна деревьям
- [ ] **Target leakage на этапе EDA** — признаки «из будущего», признаки, вычисленные с использованием таргета

## 2. Пропуски и выбросы

- [ ] **Типы пропусков** — MCAR / MAR / MNAR; почему это важно для выбора стратегии
- [ ] **Простые импутации** — mean / median / mode / константа; что они делают с распределением
- [ ] **Индикатор пропуска** — флаг `is_missing` как отдельный признак
- [ ] **Модельные импутации** — KNNImputer, IterativeImputer; риск утечки
- [ ] **Пропуски в бустингах** — XGBoost / LightGBM сами выбирают направление для NaN
- [ ] **Поиск выбросов** — IQR, z-score, Isolation Forest
- [ ] **Что делать с выбросами** — удалить / клиппинг (winsorization) / log / robust-модель; когда выброс — это сигнал

## 3. Числовые признаки

- [ ] **Зачем масштабировать** — какие модели чувствительны (линейные, kNN, SVM, нейросети, регуляризация, градиентный спуск), а какие нет (деревья)
- [ ] **Standardization (z-score)** — `(x − μ) / σ`
- [ ] **Min-Max scaling** — в [0, 1]; чувствителен к выбросам
- [ ] **Robust scaling** — median / IQR
- [ ] **Log transform** — для скошенных распределений, `log1p`
- [ ] **Power transforms** — Box-Cox (только > 0), Yeo-Johnson
- [ ] **Binning** — равные интервалы / квантили; когда полезно, что теряем
- [ ] **Ratios, differences, агрегаты** — доменные признаки (цена за м², отклонение от среднего по группе)
- [ ] **Polynomial features и interactions** — зачем линейной модели, взрыв размерности
- [ ] **Fit только на train** — scaler обучается на train и применяется к val/test

## 4. Категориальные признаки

- [ ] **One-Hot Encoding** — проблема высокой кардинальности, dummy trap (drop first)
- [ ] **Ordinal / Label encoding** — когда допустимо (порядок, деревья)
- [ ] **Frequency / Count encoding**
- [ ] **Target (mean) encoding** — сглаживание (smoothing), шум
- [ ] **Утечка в target encoding** — почему нужно out-of-fold кодирование
- [ ] **Ordered target statistics (CatBoost)** — как CatBoost решает проблему утечки
- [ ] **Hashing trick** — для очень высокой кардинальности, коллизии
- [ ] **Embeddings для категорий** — в нейросетях
- [ ] **Редкие и новые категории** — объединение в «other», обработка unseen на инференсе

## 5. Временные признаки

- [ ] **Date features** — день недели, месяц, праздники, час
- [ ] **Циклическое кодирование** — sin/cos для часа, дня недели
- [ ] **Lag features** — значение N шагов назад
- [ ] **Rolling / expanding statistics** — mean, std, min, max по окну
- [ ] **Time since event** — время с последней покупки и т.п.
- [ ] **Time leakage** — окно не должно заглядывать в будущее; split только по времени

## 6. Текст (базово, для табличных задач)

- [ ] **Bag of Words / TF-IDF** — как считается, разреженность
- [ ] **N-grams**
- [ ] **Простые текстовые признаки** — длина, число слов, наличие ключевых слов
- [ ] **Предобученные эмбеддинги как признаки**

## 7. Feature Selection

- [ ] **Зачем** — переобучение, скорость, интерпретируемость, шумовые признаки
- [ ] **Filter methods** — корреляция, MI, χ², ANOVA F-test, variance threshold
- [ ] **Wrapper methods** — forward / backward selection, RFE; стоимость
- [ ] **Embedded methods** — L1 (Lasso), feature importance в деревьях
- [ ] **Impurity-based importance** — почему смещена в пользу признаков с большим числом уникальных значений
- [ ] **Permutation importance** — как считается, проблема коррелированных признаков
- [ ] **Утечка при selection** — отбор признаков только внутри CV, иначе оценка завышена
- [ ] **Feature selection vs dimensionality reduction** — выбираем старые признаки vs создаём новые

## 8. Несбалансированные классы

- [ ] **Почему accuracy врёт** — 99% accuracy при 1% положительного класса
- [ ] **Правильные метрики** — Precision, Recall, F1, PR-AUC
- [ ] **Class weights** — как меняется loss
- [ ] **Undersampling / Oversampling**
- [ ] **SMOTE** — как генерирует точки, минусы
- [ ] **Threshold tuning** — порог 0.5 не обязателен; выбор по метрике / бизнес-стоимости
- [ ] **Cost-sensitive learning** — разная цена FP и FN
- [ ] **Утечка при resampling** — ресэмплить только train внутри фолда, не трогать val/test
- [ ] **Калибровка после ресэмплинга** — вероятности смещаются, нужна перекалибровка

---

# Часть II. Классический ML

## 9. Базовые понятия

- [ ] **Supervised / unsupervised / self-supervised / reinforcement**
- [ ] **Regression vs classification vs ranking**
- [ ] **Bias–Variance tradeoff** — разложение ошибки, underfitting vs overfitting
- [ ] **Overfitting** — признаки (train ≫ val), способы борьбы
- [ ] **Parametric vs non-parametric модели**
- [ ] **Discriminative vs generative модели**
- [ ] **No Free Lunch** — нет лучшей модели для всех задач
- [ ] **Curse of dimensionality** — расстояния теряют смысл, нужно больше данных

## 10. Линейная регрессия

- [ ] **Модель** — `y = Xw + b`, геометрический смысл
- [ ] **OLS и MSE** — почему минимизируем квадраты
- [ ] **Normal equation** — `w = (XᵀX)⁻¹Xᵀy`, когда не работает (вырожденная матрица, большая размерность)
- [ ] **Решение градиентным спуском** — когда предпочтительнее аналитического
- [ ] **Интерпретация коэффициентов** — «при прочих равных», влияние масштаба признаков
- [ ] **Предположения (Gauss–Markov)** — линейность, экзогенность, гомоскедастичность, отсутствие автокорреляции ошибок
- [ ] **Мультиколлинеарность** — нестабильные коэффициенты, VIF, лечение регуляризацией
- [ ] **Гетероскедастичность** — что это, чем плохо
- [ ] **Анализ остатков** — residual plots, что по ним видно
- [ ] **Связь MSE с нормальным шумом** — MSE = MLE при гауссовском шуме (на уровне идеи)

## 11. Логистическая регрессия

- [ ] **Модель** — линейная комбинация + sigmoid → вероятность
- [ ] **Log-odds** — интерпретация коэффициентов через отношение шансов
- [ ] **Почему не MSE** — невыпуклость с sigmoid, плохие градиенты
- [ ] **Binary cross-entropy (log loss)** — откуда берётся (MLE для Бернулли)
- [ ] **Градиент BCE** — `(p − y)·x`
- [ ] **Decision boundary** — линейная граница
- [ ] **Multiclass** — One-vs-Rest vs Softmax regression
- [ ] **Softmax и categorical cross-entropy**
- [ ] **Multilabel** — независимые sigmoid на каждый класс
- [ ] **Регуляризация в sklearn** — параметр `C = 1/λ`

## 12. kNN и Naive Bayes

- [ ] **kNN** — алгоритм, выбор k, метрики расстояния, обязательный scaling
- [ ] **kNN: минусы** — медленный инференс, проклятие размерности; ускорение (KD-tree, ANN)
- [ ] **Naive Bayes** — теорема Байеса + «наивная» независимость признаков
- [ ] **Варианты NB** — Gaussian, Multinomial (текст), Bernoulli; Laplace smoothing

## 13. SVM

- [ ] **Идея** — разделяющая гиперплоскость с максимальным зазором (margin)
- [ ] **Опорные векторы** — что это, почему модель зависит только от них
- [ ] **Hard margin vs soft margin** — параметр `C`
- [ ] **Hinge loss** — `max(0, 1 − y·f(x))`
- [ ] **Kernel trick** — переход в пространство большей размерности без явного вычисления
- [ ] **Ядра** — linear, polynomial, RBF; параметр `gamma`
- [ ] **Когда использовать** — небольшие данные, высокая размерность; плохо масштабируется на большие выборки
- [ ] **SVR** — SVM для регрессии, ε-insensitive loss

## 14. Деревья решений

- [ ] **Как строится дерево** — жадный рекурсивный выбор split
- [ ] **Критерии для классификации** — Gini, Entropy, Information Gain
- [ ] **Критерии для регрессии** — уменьшение MSE / variance
- [ ] **Как ищется лучший split** — перебор признаков и порогов
- [ ] **Предсказание в листе** — среднее / мажоритарный класс
- [ ] **Почему переобучается** — может запомнить каждую точку
- [ ] **Регуляризация** — max_depth, min_samples_leaf, min_samples_split, max_leaf_nodes
- [ ] **Pruning** — pre-pruning vs post-pruning (cost-complexity)
- [ ] **Свойства** — не нужен scaling, ловит нелинейность и взаимодействия, не экстраполирует, нестабильно

## 15. Bagging и Random Forest

- [ ] **Bootstrap** — выборка с возвращением, ~63% уникальных объектов
- [ ] **Bagging** — усреднение моделей уменьшает variance
- [ ] **Random Forest** — bagging + случайное подмножество признаков в каждом split (`max_features`)
- [ ] **Зачем декорреляция деревьев** — усреднение коррелированных моделей помогает меньше
- [ ] **OOB estimate** — бесплатная валидация на объектах, не попавших в bootstrap
- [ ] **Гиперпараметры** — n_estimators (больше не переобучает), max_features, max_depth
- [ ] **Extra Trees** — случайные пороги
- [ ] **Feature importance в RF** — impurity-based vs permutation

## 16. Boosting

### Идея

- [ ] **Boosting vs Bagging** — последовательное исправление ошибок (уменьшает bias) vs параллельное усреднение (уменьшает variance)
- [ ] **AdaBoost** — перевзвешивание ошибочных объектов (на уровне идеи)

### Gradient Boosting

- [ ] **Как работает** — каждое новое дерево обучается на антиградиент loss
- [ ] **Residuals = антиградиент MSE** — частный случай
- [ ] **Произвольный loss** — boosting для классификации, ranking, quantile
- [ ] **Learning rate (shrinkage)** — компромисс с числом деревьев
- [ ] **Number of trees + early stopping**
- [ ] **Регуляризация** — глубина, subsample (stochastic GB), colsample, min_child_weight
- [ ] **Почему переобучается в отличие от RF** — каждое дерево подгоняется под ошибки

### XGBoost

- [ ] **Второй порядок** — разложение Тейлора, используются градиент и гессиан
- [ ] **Регуляризация в объективе** — штраф за число листьев (γ) и веса листьев (λ, α)
- [ ] **Формула gain для split** — на уровне идеи
- [ ] **Обработка пропусков** — default direction
- [ ] **Рост дерева** — level-wise (по уровням)

### LightGBM

- [ ] **Leaf-wise рост** — быстрее и точнее, но легче переобучиться (`num_leaves`)
- [ ] **Histogram-based splits** — бинаризация признаков
- [ ] **GOSS** — сэмплинг объектов по величине градиента
- [ ] **EFB** — объединение разреженных взаимоисключающих признаков
- [ ] **Категориальные признаки** — нативная поддержка

### CatBoost

- [ ] **Ordered target statistics** — target encoding без утечки
- [ ] **Ordered boosting** — борьба с prediction shift
- [ ] **Symmetric (oblivious) trees** — одинаковый split на уровне; быстрый инференс, меньше переобучение
- [ ] **Комбинации категориальных признаков**
- [ ] **Почему хорошие дефолты** — часто работает «из коробки»

### Сравнение

- [ ] **XGBoost vs LightGBM vs CatBoost** — скорость, категориальные признаки, рост дерева, когда что выбирать
- [ ] **Ключевые гиперпараметры** — learning_rate, n_estimators, depth / num_leaves, subsample, colsample, reg_lambda

## 17. Другие ансамбли

- [ ] **Voting** — hard vs soft
- [ ] **Stacking** — мета-модель на предсказаниях базовых
- [ ] **OOF predictions** — почему мета-модель учат на out-of-fold, а не на train-предсказаниях
- [ ] **Blending** — отличие от stacking (hold-out)
- [ ] **Почему ансамбли работают** — разнообразие ошибок моделей

---

# Часть III. Как модель учится

## 18. Loss functions

### Регрессия

- [ ] **MSE** — штрафует большие ошибки, чувствителен к выбросам, оптимум — среднее
- [ ] **MAE** — устойчив к выбросам, оптимум — медиана, негладкий в нуле
- [ ] **Huber** — компромисс MSE и MAE
- [ ] **Quantile (pinball) loss** — предсказание квантилей, интервалы
- [ ] **Log-cosh, MSLE** — когда важна относительная ошибка

### Классификация

- [ ] **Binary cross-entropy**
- [ ] **Categorical cross-entropy** — связь с softmax и KL-дивергенцией
- [ ] **Hinge loss** — SVM
- [ ] **Focal loss** — фокус на сложных примерах, дисбаланс
- [ ] **Label smoothing**

### Прочее

- [ ] **Ranking losses** — pairwise (RankNet), listwise (LambdaRank)
- [ ] **Contrastive / triplet loss** — обучение эмбеддингов
- [ ] **Loss ≠ метрика** — оптимизируем дифференцируемый суррогат, оцениваем бизнес-метрикой

## 19. Оптимизация

- [ ] **Градиент** — направление наискорейшего роста
- [ ] **Gradient Descent** — шаг против градиента
- [ ] **Learning rate** — слишком большой (расходится) / маленький (медленно)
- [ ] **Batch / Mini-batch / SGD** — компромисс точности градиента и скорости, шум как регуляризатор
- [ ] **Выпуклость** — почему у линейной/логистической регрессии один минимум, а у нейросетей нет
- [ ] **Локальные минимумы и седловые точки**
- [ ] **Momentum** — накопление скорости, гашение осцилляций
- [ ] **Nesterov momentum**
- [ ] **AdaGrad / RMSProp** — адаптивный lr для каждого параметра
- [ ] **Adam** — momentum + RMSProp + bias correction
- [ ] **AdamW** — почему weight decay ≠ L2 в Adam
- [ ] **Learning rate schedules** — step decay, cosine, warmup, OneCycle
- [ ] **Методы второго порядка** — Ньютон, почему редко используются в DL (гессиан)

## 20. Регуляризация (классический ML)

- [ ] **Зачем** — ограничение сложности модели, борьба с переобучением
- [ ] **L2 / Ridge** — сжимает веса, устойчивость к мультиколлинеарности
- [ ] **L1 / Lasso** — зануляет веса → отбор признаков
- [ ] **Почему L1 зануляет** — геометрия (ромб vs круг), субградиент
- [ ] **Elastic Net** — L1 + L2, группы коррелированных признаков
- [ ] **Регуляризация и scaling** — почему без масштабирования штраф несправедлив
- [ ] **Байесовский взгляд** — L2 = гауссовский prior, L1 = Лаплас (на уровне идеи)
- [ ] **Early stopping** — как форма регуляризации

---

# Часть IV. Оценка и валидация

## 21. Метрики регрессии

- [ ] **MAE, MSE, RMSE** — разница, чувствительность к выбросам
- [ ] **R²** — доля объяснённой дисперсии, может быть < 0
- [ ] **Adjusted R²**
- [ ] **MAPE / SMAPE / WAPE** — проблемы MAPE (нули, асимметрия)
- [ ] **Какую метрику выбрать** — под бизнес-задачу

## 22. Метрики классификации

- [ ] **Confusion matrix** — TP, FP, TN, FN
- [ ] **Accuracy** — когда бесполезна
- [ ] **Precision / Recall** — когда что важнее (спам vs болезнь)
- [ ] **F1, F-beta** — гармоническое среднее, вес recall
- [ ] **ROC-кривая и ROC-AUC** — вероятностная интерпретация (ранжирование пары)
- [ ] **PR-кривая и PR-AUC** — почему лучше ROC-AUC при дисбалансе
- [ ] **Log loss** — как метрика качества вероятностей
- [ ] **Multiclass averaging** — macro / micro / weighted
- [ ] **Выбор порога** — по метрике, по бизнес-стоимости ошибок

## 23. Калибровка вероятностей

- [ ] **Что такое калибровка** — предсказанная вероятность = реальная частота
- [ ] **Reliability diagram, Brier score**
- [ ] **Какие модели плохо откалиброваны** — SVM, бустинги, RF, NB, ресэмплинг
- [ ] **Platt scaling** — логистическая регрессия поверх скоров
- [ ] **Isotonic regression** — непараметрически, нужно больше данных
- [ ] **Temperature scaling** — для нейросетей

## 24. Валидация

- [ ] **Train / validation / test** — роль каждой части
- [ ] **K-Fold**
- [ ] **Stratified K-Fold** — сохранение пропорций классов
- [ ] **Group K-Fold** — объекты одного пользователя не должны попасть в train и val одновременно
- [ ] **Time Series Split** — только прошлое → будущее, gap
- [ ] **Nested CV** — честная оценка при подборе гиперпараметров
- [ ] **Preprocessing внутри CV** — Pipeline в sklearn, fit только на train-части фолда
- [ ] **Виды утечек** — target leakage, train-test contamination, temporal leakage, дубликаты
- [ ] **Learning curves** — диагностика: больше данных или сложнее модель
- [ ] **Validation curves** — зависимость качества от гиперпараметра

## 25. Подбор гиперпараметров

- [ ] **Параметры vs гиперпараметры**
- [ ] **Grid Search** — полный перебор, дорого
- [ ] **Random Search** — почему часто эффективнее grid
- [ ] **Bayesian Optimization** — суррогатная модель + acquisition function
- [ ] **Optuna / TPE** — как работает, pruning плохих trials
- [ ] **Search space** — log-шкала для lr и регуляризации
- [ ] **Early stopping**
- [ ] **Почему нельзя тюнить на test** — оптимистичная оценка

## 26. Интерпретируемость

- [ ] **Global vs local объяснения**
- [ ] **Коэффициенты линейных моделей** — и почему им нельзя слепо верить
- [ ] **Feature importance** — impurity vs permutation
- [ ] **SHAP** — идея значений Шепли, аддитивность, TreeSHAP
- [ ] **LIME** — локальная линейная аппроксимация
- [ ] **Partial Dependence Plots / ICE**

---

# Часть V. Обучение без учителя

## 27. Кластеризация

- [ ] **K-Means** — алгоритм (assign → update), objective (inertia)
- [ ] **K-Means++** — инициализация центров
- [ ] **Ограничения K-Means** — сферические кластеры, чувствителен к масштабу и выбросам, нужно знать k
- [ ] **Выбор числа кластеров** — elbow method, silhouette score
- [ ] **Hierarchical clustering** — agglomerative, linkage (single / complete / average / ward), дендрограмма
- [ ] **DBSCAN** — eps, min_samples, кластеры произвольной формы, шум
- [ ] **Gaussian Mixture Models** — мягкая кластеризация, EM (на уровне идеи)

## 28. Снижение размерности

- [ ] **PCA: идея** — направления максимальной дисперсии
- [ ] **PCA: как считается** — центрирование, ковариационная матрица, собственные векторы / SVD
- [ ] **Explained variance** — как выбрать число компонент
- [ ] **Scaling перед PCA** — обязателен
- [ ] **Ограничения PCA** — только линейные зависимости, потеря интерпретируемости
- [ ] **t-SNE** — для визуализации, сохраняет локальную структуру, расстояния между кластерами бессмысленны
- [ ] **UMAP** — быстрее t-SNE, лучше сохраняет глобальную структуру
- [ ] **Autoencoders** — нелинейное снижение размерности

## 29. Поиск аномалий

- [ ] **Статистические методы** — z-score, IQR
- [ ] **Isolation Forest** — аномалии изолируются за меньшее число разбиений
- [ ] **One-Class SVM**
- [ ] **LOF** — локальная плотность
- [ ] **Autoencoder reconstruction error**

---

# Часть VI. Deep Learning

## 30. MLP и основы

- [ ] **Перцептрон и MLP** — слои, веса, bias
- [ ] **Зачем нелинейность** — без неё сеть схлопывается в линейную модель
- [ ] **Universal approximation theorem** — на уровне идеи
- [ ] **Forward pass**
- [ ] **Backpropagation** — chain rule, вычислительный граф
- [ ] **Autograd** — как работает в PyTorch

## 31. Функции активации

- [ ] **Sigmoid** — насыщение, затухающие градиенты, не центрирована
- [ ] **Tanh** — центрирована, но тоже насыщается
- [ ] **ReLU** — быстрая, нет насыщения при x > 0, dying ReLU
- [ ] **Leaky ReLU / PReLU / ELU**
- [ ] **GELU / SiLU (Swish)** — в трансформерах
- [ ] **Softmax** — на выходе для multiclass, численная стабильность (вычитание max)
- [ ] **Выбор активации на выходе** — под задачу и loss

## 32. Проблемы обучения глубоких сетей

- [ ] **Vanishing / exploding gradients** — причины
- [ ] **Инициализация весов** — Xavier/Glorot, He/Kaiming; почему нельзя нули
- [ ] **Gradient clipping**
- [ ] **Residual connections** — почему помогают обучать глубокие сети

## 33. Нормализация

- [ ] **Batch Normalization** — как работает, train vs inference (running stats), зависимость от размера батча
- [ ] **Layer Normalization** — почему в трансформерах и RNN
- [ ] **RMSNorm, Group / Instance Norm**
- [ ] **Pre-norm vs post-norm**

## 34. Регуляризация в DL

- [ ] **Dropout** — как работает, train vs inference, inverted dropout
- [ ] **Weight decay**
- [ ] **Data augmentation**
- [ ] **Early stopping**
- [ ] **Label smoothing**
- [ ] **Double descent** — на уровне идеи

## 35. Практика обучения

- [ ] **Training loop** — forward, loss, backward, step, zero_grad
- [ ] **Выбор batch size и lr** — связь между ними
- [ ] **LR finder, warmup**
- [ ] **Mixed precision (fp16 / bf16)**
- [ ] **Диагностика** — loss не падает / NaN / переобучение; overfit на одном батче как sanity check

## 36. CNN

- [ ] **Свёртка** — kernel, stride, padding, количество параметров
- [ ] **Receptive field**
- [ ] **Pooling** — max / average / global average pooling
- [ ] **Inductive bias** — локальность, инвариантность к сдвигу
- [ ] **Архитектуры** — LeNet → AlexNet → VGG → ResNet → EfficientNet (ключевая идея каждой)
- [ ] **1×1 свёртки**
- [ ] **Depthwise separable convolutions**

## 37. RNN

- [ ] **Vanilla RNN** — скрытое состояние, BPTT
- [ ] **Проблема длинных зависимостей**
- [ ] **LSTM** — гейты (forget, input, output), cell state
- [ ] **GRU** — упрощённый LSTM
- [ ] **Bidirectional RNN, seq2seq**

## 38. Attention и Transformers

- [ ] **Attention** — query, key, value
- [ ] **Scaled dot-product attention** — зачем делить на √d
- [ ] **Self-attention vs cross-attention**
- [ ] **Multi-head attention**
- [ ] **Positional encoding** — sinusoidal, learned, RoPE
- [ ] **Блок трансформера** — attention + FFN + residual + LayerNorm
- [ ] **Encoder / Decoder / Encoder-Decoder** — BERT / GPT / T5
- [ ] **Causal masking**
- [ ] **Сложность O(n²)** — по длине последовательности, способы обхода
- [ ] **KV-cache** — ускорение генерации

## 39. Эмбеддинги и representation learning

- [ ] **Что такое эмбеддинг** — плотное представление объекта
- [ ] **Word2Vec** — CBOW, Skip-gram, negative sampling
- [ ] **Contrastive learning** — SimCLR, CLIP (на уровне идеи)
- [ ] **Метрики близости** — cosine, dot product
- [ ] **Approximate Nearest Neighbors** — FAISS, HNSW

## 40. Transfer learning и fine-tuning

- [ ] **Transfer learning** — использование предобученной модели
- [ ] **Feature extraction vs fine-tuning**
- [ ] **Заморозка слоёв, разные lr для слоёв**
- [ ] **PEFT / LoRA** — обучение небольшого числа параметров

## 41. Генеративные модели (обзорно)

- [ ] **Autoencoder и VAE** — латентное пространство, reparametrization trick
- [ ] **GAN** — генератор vs дискриминатор, mode collapse
- [ ] **Diffusion models** — постепенное зашумление и обучение денойзингу
- [ ] **Авторегрессионные модели** — генерация токен за токеном

---

# Часть VII. Прикладные области

## 42. NLP

- [ ] **Токенизация** — word / subword (BPE, WordPiece)
- [ ] **TF-IDF → Word2Vec → BERT** — эволюция представлений текста
- [ ] **BERT** — MLM, fine-tuning под классификацию
- [ ] **GPT / LLM** — next-token prediction, decoding (greedy, beam, top-k, top-p, temperature)
- [ ] **Instruction tuning, RLHF** — на уровне идеи
- [ ] **RAG** — retrieval + генерация

## 43. Computer Vision

- [ ] **Классификация** — ResNet, ViT
- [ ] **Детекция** — two-stage vs one-stage (Faster R-CNN, YOLO), IoU, NMS, mAP
- [ ] **Сегментация** — semantic / instance, U-Net
- [ ] **Аугментации** — flip, crop, color jitter, mixup, cutmix

## 44. Ранжирование и рекомендации

- [ ] **Двухэтапная схема** — candidate generation → ranking
- [ ] **Collaborative filtering** — user-based, item-based
- [ ] **Matrix factorization** — ALS, SVD-подходы
- [ ] **Content-based рекомендации**
- [ ] **Two-tower модели**
- [ ] **Learning to Rank** — pointwise / pairwise / listwise
- [ ] **Метрики** — Precision@K, Recall@K, MAP, MRR, NDCG
- [ ] **Cold start** — новые пользователи и объекты
- [ ] **Implicit vs explicit feedback**
- [ ] **Beyond accuracy** — diversity, novelty, popularity bias

## 45. Временные ряды

- [ ] **Компоненты ряда** — тренд, сезонность, шум
- [ ] **Стационарность** — зачем, differencing, тест ADF
- [ ] **ACF / PACF**
- [ ] **AR, MA, ARIMA, SARIMA** — на уровне идеи
- [ ] **Exponential smoothing**
- [ ] **ML-подход** — lag / rolling признаки + бустинг
- [ ] **Валидация** — expanding / sliding window, без перемешивания
- [ ] **Метрики прогноза** — MAE, MAPE, sMAPE, MASE
- [ ] **Горизонт прогноза** — recursive vs direct

---

# Часть VIII. Продакшн

## 46. Эксперименты и A/B тесты

- [ ] **Offline vs online метрики** — почему offline-рост не гарантирует рост в A/B
- [ ] **Дизайн A/B теста** — гипотеза, метрика, единица рандомизации
- [ ] **p-value и статистическая значимость** — что это на самом деле значит
- [ ] **Ошибки I и II рода, power**
- [ ] **MDE и размер выборки**
- [ ] **Практическая vs статистическая значимость**
- [ ] **Подводные камни** — peeking, multiple testing, novelty effect, network effects

## 47. ML System Design

- [ ] **Постановка задачи** — бизнес-цель → ML-задача → target → метрики
- [ ] **Данные** — источники, разметка, качество
- [ ] **Baseline** — эвристика или простая модель
- [ ] **Training pipeline** — воспроизводимость, версионирование данных и моделей
- [ ] **Batch vs online inference**
- [ ] **Offline / online features, Feature Store** — training-serving skew
- [ ] **Latency, throughput, scalability**
- [ ] **Оптимизация инференса** — quantization, pruning, distillation, ONNX
- [ ] **Model serving** — REST / gRPC, model registry
- [ ] **Деплой** — shadow, canary, A/B
- [ ] **Мониторинг** — качество, data drift, concept drift
- [ ] **Retraining** — по расписанию / по триггеру
- [ ] **Feedback loops** — модель влияет на собственные будущие данные

## 48. Практика (уметь сделать руками)

- [ ] Линейная регрессия на NumPy (GD + normal equation)
- [ ] Логистическая регрессия на NumPy
- [ ] Метрики с нуля (precision, recall, ROC-AUC)
- [ ] K-Means с нуля
- [ ] Decision tree split с нуля
- [ ] MLP с backprop на NumPy
- [ ] Честный pipeline: preprocessing + модель + CV без утечек
- [ ] Найти утечку в чужом коде
- [ ] Выбрать метрику и порог под бизнес-задачу
- [ ] Объяснить, почему модель переобучилась и что делать
