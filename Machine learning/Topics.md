# Roadmap: Data Scientist / ML Engineer

  
# Часть I. Основы ML

  

# 1. Базовые понятия

  

* [ ] ⭐ Supervised / Unsupervised / Self-supervised / Reinforcement learning
* [ ] Regression / Classification / Ranking / Clustering — постановки задач

* [ ] Parametric vs Non-parametric модели

* [ ] Generative vs Discriminative модели

* [ ] ⭐ Generalization, Underfitting / Overfitting

* [x] ⭐ Bias-Variance tradeoff

* [ ] ⭐ MLE → откуда берутся MSE (Gaussian) и BCE (Bernoulli)

* [ ] MAP → откуда берутся L2 (Gaussian prior) и L1 (Laplace prior)

* [ ] Empirical risk minimization

* [ ] Curse of dimensionality

* [ ] No Free Lunch — на уровне идеи

  

### Data Leakage ⭐

  

* [ ] Target leakage

* [ ] Train-test contamination

* [ ] Temporal leakage

* [ ] Leakage через preprocessing / feature selection / resampling

* [ ] Как находить leakage (слишком хорошие метрики, feature importance)

  

### Работа с данными

  

* [ ] EDA: распределения, корреляции, выбросы

* [ ] Пропуски: MCAR / MAR / MNAR

* [ ] Imputation: mean / median / mode / model-based / indicator-признак

* [ ] Outliers: IQR, z-score, что с ними делать

* [ ] Дубликаты, шум в разметке (label noise)

* [ ] Train / test distribution shift

  

---

  

# Часть II. Classical ML

  

# 2. Linear Regression

  

* [x] Что такое linear regression

* [x] OLS

* [x] Normal equation

* [x] Геометрический смысл OLS

* [x] Gradient Descent

* [x] MSE

* [x] Интерпретация коэффициентов

* [x] Exogeneity

* [x] Gauss-Markov assumptions

* [x] Bias

* [x] Unbiased estimator

* [ ] ⭐ Multicollinearity, VIF, почему это проблема

* [ ] Heteroscedasticity

* [ ] Autocorrelation

* [ ] Residual analysis

* [ ] Polynomial regression

* [ ] Ridge — closed-form решение, почему решает проблему вырожденной матрицы

* [ ] Чувствительность к выбросам, Huber loss

* [ ] Quantile regression — базово

  

### Regression Metrics

  

* [x] MAE

* [x] MSE

* [x] RMSE

* [x] R²

* [ ] Adjusted R²

* [ ] MAPE, SMAPE, WAPE

* [ ] MSLE / RMSLE

* [ ] ⭐ MAE → медиана, MSE → среднее (что оптимизирует каждая)

* [ ] ⭐ Когда какую использовать

  

---

  

# 3. Classification

  

### Logistic Regression

  

* [x] Linear classifier

* [x] Sigmoid

* [x] BCE

* [x] Derivation BCE

* [x] Gradient

* [x] Multiclass softmax

* [x] Cross-entropy

* [ ] ⭐ Почему не MSE для классификации

* [ ] Интерпретация коэффициентов через log-odds

* [ ] Decision boundary, линейная разделимость

* [ ] One-vs-Rest / One-vs-One

* [ ] Multilabel classification

  

### Metrics

  

* [x] Confusion Matrix

* [x] Accuracy

* [x] Precision

* [x] Recall

* [x] F1

* [x] ROC

* [x] ROC-AUC

* [x] PR-AUC ✅ 2026-09-29

* [x] Когда ROC-AUC плох ✅ 2026-09-29

* [x] Calibration ✅ 2026-09-29

* [x] Platt scaling — базово

* [ ] ⭐ Вероятностный смысл ROC-AUC

* [ ] F-beta

* [ ] Micro / Macro / Weighted averaging

* [ ] Log-loss как метрика, Brier score

* [ ] Isotonic regression

* [ ] Gini = 2·AUC − 1, Lift

* [ ] MCC — базово

* [ ] ⭐ Выбор порога под бизнес-задачу

  

---

  

# 4. SVM

  

* [ ] ⭐ Maximum margin

* [ ] Hard / Soft margin

* [ ] Hinge loss

* [ ] Параметр C

* [ ] Support vectors

* [ ] ⭐ Kernel trick

* [ ] Linear / Polynomial / RBF kernel

* [ ] Dual problem — на уровне идеи

* [ ] SVM vs Logistic Regression

  

---

  

# 5. kNN

  

* [ ] Алгоритм, lazy learning

* [ ] Метрики расстояния: Euclidean, Manhattan, Cosine

* [ ] Выбор k, weighted kNN

* [ ] Почему нужен scaling

* [ ] Curse of dimensionality

* [ ] Сложность predict, KD-tree / Ball-tree

* [ ] Approximate Nearest Neighbors (связь с RAG)

  

---

  

# 6. Naive Bayes

  

* [ ] Наивное предположение о независимости

* [ ] Gaussian / Multinomial / Bernoulli NB

* [ ] Laplace smoothing

* [ ] Применение для текстов

  

---

  

# 7. Trees

  

* [x] Decision Tree

* [x] Classification tree

* [x] Regression tree

* [x] Gini

* [x] Entropy ✅ 2026-09-29

* [x] Information Gain ✅ 2026-09-29

* [x] Как выбирается split ✅ 2026-09-29

* [x] Overfitting trees

* [x] Tree depth

* [x] Pruning ✅ 2026-09-28

* [ ] Почему деревьям не нужен scaling

* [ ] Деревья не умеют экстраполировать

* [ ] Обработка пропусков и категориальных признаков

* [ ] Сложность построения дерева

  

### Random Forest

  

* [x] Bagging

* [x] Random Forest

* [x] Bootstrap

* [x] Random feature selection

* [ ] OOB estimate

* [ ] ⭐ Почему RF уменьшает variance (декорреляция деревьев)

* [ ] Основные гиперпараметры RF

* [ ] Bias MDI feature importance

* [ ] Extra Trees

  

---

  

# 8. Boosting

  

* [x] Основная идея boosting

* [x] Gradient Boosting

* [x] Residuals

* [x] Negative gradient

* [x] Learning rate

* [x] Number of trees

* [x] Second-order intuition

* [ ] AdaBoost — идея

* [ ] ⭐ Boosting vs Bagging: bias vs variance

* [ ] Гиперпараметры: depth, subsample, colsample, min_child_weight, early stopping

* [ ] XGBoost

* [ ] XGBoost regularization

* [ ] Histogram-based splits

* [ ] LightGBM: leaf-wise рост, GOSS, EFB

* [ ] CatBoost: oblivious trees, ordered boosting

* [ ] Почему CatBoost хорош для категориальных признаков (ordered target statistics)

* [ ] ⭐ Отличия XGBoost / LightGBM / CatBoost

* [ ] Почему бустинг на табличных данных обычно лучше нейросетей

  

---

  

# 9. Regularization

  

* [x] Overfitting

* [x] Bias-Variance

* [x] L1 / Lasso

* [x] L2 / Ridge

* [x] Elastic Net

* [x] Weight decay

* [x] Почему scaling важен для regularization ✅ 2026-09-28

* [ ] Геометрическая интерпретация L1/L2

* [ ] ⭐ Почему L1 зануляет коэффициенты

  

---

  

# 10. Feature Engineering

  

### Numerical

  

* [x] Scaling ✅ 2026-09-29

* [x] Standardization ✅ 2026-09-29

* [x] Min-Max ✅ 2026-09-29

* [x] Robust scaling ✅ 2026-09-29

* [x] Log transform ✅ 2026-09-29

* [x] Power transforms ✅ 2026-09-29

* [x] Binning ✅ 2026-09-29

* [x] Ratios ✅ 2026-09-29

* [x] Differences ✅ 2026-09-29

  

### Categorical

  

* [x] One-Hot ✅ 2026-09-29

* [x] Ordinal encoding ✅ 2026-09-29

* [x] Target encoding ✅ 2026-09-29

* [x] Frequency encoding ✅ 2026-09-29

* [x] Leakage при target encoding ✅ 2026-09-29

* [ ] High-cardinality признаки, hashing trick

* [ ] Embeddings для категорий

  

### Interactions

  

* [ ] Polynomial features

* [ ] Interaction terms

* [ ] Каким моделям нужны interactions, а каким нет

  

### Time

  

* [ ] Date features, cyclical encoding (sin/cos)

* [ ] Lag

* [ ] Rolling mean

* [ ] Rolling statistics

* [ ] Time leakage

  

### Text (классические признаки)

  

* [ ] Bag of Words, n-grams

* [ ] TF-IDF

  

---

  

# 11. Feature Selection

  

* [x] Filter methods

* [x] Correlation

* [x] Mutual Information

* [x] Statistical tests

* [x] Wrapper methods

* [x] RFE

* [x] Embedded methods

* [x] Lasso

* [x] Tree feature importance

* [x] Permutation importance

* [x] Leakage при feature selection

* [ ] Более глубокие нюансы selection + CV

  

---

  

# 12. Interpretability

  

* [ ] Global vs Local интерпретация

* [ ] Коэффициенты линейных моделей

* [ ] Feature importance: MDI vs Permutation

* [ ] ⭐ SHAP: идея Shapley values, TreeSHAP

* [ ] LIME

* [ ] PDP / ICE

* [ ] Почему важность ≠ причинность

  

---

  

# 13. Dimensionality Reduction

  

* [ ] ⭐ PCA

* [ ] Как выводится PCA

* [ ] Variance maximization

* [ ] Covariance matrix

* [ ] Eigenvectors

* [ ] Explained variance

* [ ] SVD

* [ ] Когда PCA полезен

* [ ] Ограничения PCA

* [ ] PCA vs Feature Selection

* [ ] t-SNE — концептуально

* [ ] UMAP — концептуально

* [ ] Autoencoders как нелинейное снижение размерности

  

---

  

# 14. Unsupervised Learning

  

### Clustering

  

* [ ] ⭐ K-Means

* [ ] Objective function

* [ ] Как выбирается центр

* [ ] K-Means++

* [ ] Ограничения K-Means (форма кластеров, scaling, выбросы)

* [ ] Elbow method

* [ ] Silhouette score

* [ ] Hierarchical clustering, linkage

* [ ] DBSCAN

* [ ] GMM и EM-алгоритм — базово

  

### Anomaly Detection

  

* [ ] Isolation Forest

* [ ] LOF

* [ ] One-Class SVM

* [ ] Статистические методы (z-score, IQR)

  

---

  

# 15. Imbalanced Classification

  

* [x] Что такое class imbalance ✅ 2026-09-29

* [x] Почему Accuracy может быть бесполезной ✅ 2026-09-29

* [x] Precision / Recall ✅ 2026-09-29

* [x] PR-AUC ✅ 2026-09-29

* [x] Class weights ✅ 2026-09-29

* [x] Oversampling ✅ 2026-09-29

* [x] Undersampling ✅ 2026-09-29

* [x] SMOTE ✅ 2026-09-29

* [x] Threshold tuning ✅ 2026-09-29

* [x] Cost-sensitive learning ✅ 2026-09-29

* [x] Leakage при resampling ✅ 2026-09-29

* [ ] Focal loss (связь с DL)

  

---

  

# 16. Cross-Validation

  

* [x] K-Fold

* [x] Stratified K-Fold

* [x] Train / validation / test

* [x] Nested CV

* [x] Group K-Fold ✅ 2026-09-29

* [x] Time Series Split ✅ 2026-09-29

* [x] Почему preprocessing должен быть внутри CV ✅ 2026-09-29

* [x] Feature selection внутри CV ✅ 2026-09-29

* [x] Hyperparameter tuning + CV ✅ 2026-09-29

* [ ] Adversarial validation

  

---

  

# 17. Hyperparameter Optimization

  

* [x] Grid Search ✅ 2026-09-29

* [x] Random Search ✅ 2026-09-29

* [x] Bayesian Optimization ✅ 2026-09-29

* [x] Optuna ✅ 2026-09-29

* [x] Что такое search space ✅ 2026-09-29

* [x] Почему нельзя подбирать гиперпараметры на test ✅ 2026-09-29

* [x] Early stopping ✅ 2026-09-29

  

---

  

# 18. Ensemble Methods

  

* [x] Bagging

* [x] Random Forest

* [x] Boosting

* [x] Stacking

* [x] Blending

* [x] OOF predictions

* [ ] Voting

* [ ] Hard / Soft voting

* [ ] Почему ансамбли работают (разнообразие моделей)

  

---

  

# 19. Ranking / Recommendation

  

### Ranking

  

* [ ] Pointwise ranking

* [ ] Pairwise ranking

* [ ] Listwise ranking

* [ ] LambdaRank / LambdaMART

* [ ] YetiRank (CatBoost), XGBRanker / LGBMRanker

* [x] Ranking metrics ✅ 2026-09-29

* [x] NDCG ✅ 2026-09-29

* [x] MAP ✅ 2026-09-29

* [x] MRR ✅ 2026-09-29

* [x] Precision@K ✅ 2026-09-29

* [x] Recall@K ✅ 2026-09-29

  

### Recommender Systems

  

* [x] Recommendation basics ✅ 2026-09-29

* [x] Candidate generation ✅ 2026-09-29

* [x] Ranking stage ✅ 2026-09-29

* [ ] Explicit vs Implicit feedback

* [ ] Content-based

* [ ] ⭐ Collaborative filtering: user-based / item-based

* [ ] Matrix factorization, ALS

* [ ] Two-tower модели, item/user embeddings

* [ ] Negative sampling

* [ ] Cold start (user / item)

* [ ] Popularity bias, diversity, novelty, coverage

* [ ] Offline vs Online метрики (CTR, конверсия)

  

---

  

# 20. Time Series

  

* [ ] Train/test split во времени

* [ ] Trend

* [ ] Seasonality

* [ ] Stationarity, differencing

* [ ] Lag features

* [ ] Rolling features

* [ ] AR

* [ ] MA

* [ ] ARIMA — базово

* [ ] Exponential smoothing

* [ ] Бустинг для временных рядов

* [ ] Recursive vs Direct multi-step forecasting

* [ ] Time series CV

* [ ] Forecasting metrics (MAE, MAPE, WAPE, MASE)

  

---

  

# Часть III. Deep Learning

  

# 21. Основы нейросетей

  

* [ ] Perceptron, MLP

* [ ] Universal approximation theorem — идея

* [ ] ⭐ Forward / Backward pass, computational graph

* [ ] ⭐ Backpropagation, chain rule (уметь посчитать руками для маленькой сети)

* [ ] Activations: Sigmoid, Tanh, ReLU, LeakyReLU, GELU, SiLU/Swish, Softmax

* [ ] ⭐ Vanishing / Exploding gradients

* [ ] Weight initialization: Xavier, He

* [ ] Loss functions: MSE, CE, Focal, Contrastive, Triplet

* [ ] Embeddings

  

### Optimization

  

* [x] Loss function

* [x] Gradient Descent

* [x] Learning rate

* [x] Batch / Mini-batch / SGD ✅ 2026-10-01

* [x] Momentum ✅ 2026-10-01

* [x] Adam ✅ 2026-10-01

* [x] Convexity

* [ ] Nesterov, AdaGrad, RMSProp

* [ ] ⭐ AdamW — чем отличается от Adam + L2

* [ ] LR schedulers: step, cosine, warmup, OneCycle

* [ ] Gradient clipping

* [ ] Влияние batch size

* [ ] Невыпуклость, локальные минимумы, седловые точки

  

### Regularization & Normalization

  

* [ ] ⭐ Dropout (поведение в train / eval)

* [x] Weight decay

* [ ] Early stopping

* [ ] Data augmentation

* [ ] Label smoothing

* [ ] ⭐ BatchNorm (train vs inference, running stats)

* [ ] LayerNorm, RMSNorm, GroupNorm

* [ ] BatchNorm vs LayerNorm — когда что

* [ ] Residual connections — зачем

  

### Практика (PyTorch)

  

* [ ] Tensors, autograd

* [ ] nn.Module, Dataset, DataLoader

* [ ] Training loop с нуля

* [ ] model.train() / model.eval(), torch.no_grad()

* [ ] GPU, mixed precision (fp16 / bf16)

* [ ] Gradient accumulation

* [ ] Debugging: overfit one batch, проверка loss в начале обучения

* [ ] Transfer Learning

* [ ] Fine-tuning: freeze / unfreeze, разные LR для слоёв

  

---

  

# 22. Computer Vision

  

### CNN

  

* [ ] ⭐ Convolution: kernel, stride, padding, dilation

* [ ] ⭐ Расчёт размера выхода и числа параметров

* [ ] Receptive field

* [ ] Pooling (max / avg / global)

* [ ] 1×1 convolution, depthwise separable convolution

* [ ] Почему CNN лучше MLP для изображений (inductive bias)

  

### Архитектуры

  

* [ ] LeNet, AlexNet, VGG — эволюция

* [ ] ⭐ ResNet — зачем skip connections

* [ ] Inception

* [ ] MobileNet, EfficientNet

* [ ] Vision Transformer (ViT)

* [ ] ConvNeXt — базово

  

### Задачи

  

* [ ] Classification

* [ ] Object Detection: two-stage (R-CNN → Faster R-CNN) vs one-stage (YOLO, SSD)

* [ ] Anchors, ⭐ IoU, ⭐ NMS, mAP

* [ ] DETR — идея

* [ ] Segmentation: semantic / instance / panoptic

* [ ] U-Net, FCN, Mask R-CNN

* [ ] Dice loss, IoU для сегментации

* [ ] SAM — базово

* [ ] Metric learning: Triplet loss, ArcFace

  

### Self-supervised & Multimodal

  

* [ ] Contrastive learning: SimCLR

* [ ] DINO — базово

* [ ] ⭐ CLIP

  

### Генеративные модели

  

* [ ] Autoencoder

* [ ] VAE: reparameterization trick, ELBO — идея

* [ ] GAN: generator / discriminator, mode collapse

* [ ] Diffusion models — идея (forward / reverse process)

  

### Практика

  

* [ ] Augmentations (flip, crop, color jitter, mixup, cutmix)

* [ ] Работа с несбалансированными классами в CV

  

---

  

# 23. NLP

  

### Классический NLP

  

* [ ] Tokenization, lemmatization / stemming, stop words

* [ ] Bag of Words, TF-IDF, n-grams

* [ ] ⭐ Word2Vec: CBOW, Skip-gram, negative sampling

* [ ] GloVe, FastText (subword-информация)

  

### RNN

  

* [ ] RNN, BPTT

* [ ] Vanishing gradient в RNN

* [ ] ⭐ LSTM, GRU — гейты

* [ ] Bidirectional RNN

* [ ] Seq2Seq, encoder-decoder

* [ ] Attention Bahdanau / Luong — откуда появился attention

* [ ] Beam search

  

### Subword Tokenization

  

* [ ] ⭐ BPE

* [ ] WordPiece, SentencePiece / Unigram

* [ ] Проблемы токенизации (OOV, многоязычность, числа)

  

### Pretrained модели

  

* [ ] ⭐ Encoder-only (BERT) / Decoder-only (GPT) / Encoder-Decoder (T5)

* [ ] BERT: MLM, NSP, [CLS]-токен

* [ ] RoBERTa, DistilBERT — что изменили

* [ ] Sentence embeddings: Sentence-BERT, contrastive обучение

  

### Задачи и метрики

  

* [ ] Text classification

* [ ] NER, sequence labeling

* [ ] Question Answering

* [ ] Summarization, Machine Translation

* [ ] Metrics: BLEU, ROUGE, ⭐ Perplexity

  

---

  

# 24. Transformers

  

* [ ] ⭐ Self-attention: Q, K, V

* [ ] ⭐ Scaled dot-product attention — зачем делить на √d

* [ ] ⭐ Multi-head attention

* [ ] Masking: causal, padding

* [ ] Cross-attention

* [ ] Positional encoding: sinusoidal, learned, ⭐ RoPE, ALiBi

* [ ] Transformer block: attention + FFN + residual + LayerNorm

* [ ] Pre-LN vs Post-LN

* [ ] ⭐ Сложность O(n²) по длине последовательности

* [ ] Подсчёт числа параметров трансформера

* [ ] ⭐ KV-cache

* [ ] MQA / GQA

* [ ] FlashAttention — идея

* [ ] Sparse / Linear attention — базово

* [ ] Mixture of Experts (MoE)

  

---

  

# 25. LLM

  

### Pretraining

  

* [ ] ⭐ Causal language modeling, next-token prediction

* [ ] Scaling laws (Chinchilla)

* [ ] Данные для претрейна, дедупликация, фильтрация

* [ ] Context window, long context

  

### Generation / Decoding

  

* [ ] Greedy, Beam search

* [ ] ⭐ Temperature, Top-k, Top-p (nucleus)

* [ ] Repetition penalty

* [ ] Structured output (JSON, constrained decoding)

  

### Fine-tuning

  

* [ ] SFT, instruction tuning

* [ ] ⭐ PEFT: LoRA, QLoRA

* [ ] Adapters, Prefix / Prompt tuning

* [ ] Catastrophic forgetting

* [ ] ⭐ Когда fine-tuning, а когда RAG / prompting

  

### Alignment

  

* [ ] ⭐ RLHF: reward model, PPO

* [ ] DPO

* [ ] GRPO, RLAIF — базово

  

### Prompting

  

* [ ] Zero-shot / Few-shot, in-context learning

* [ ] Chain-of-Thought

* [ ] System prompts, prompt templates

* [ ] Reasoning-модели — идея

  

### Inference Optimization

  

* [ ] ⭐ Quantization: INT8 / INT4, GPTQ, AWQ

* [ ] KV-cache, PagedAttention (vLLM)

* [ ] Continuous batching

* [ ] Speculative decoding

* [ ] Knowledge distillation

* [ ] Метрики: latency, TTFT, tokens/sec, стоимость

  

### Agents

  

* [ ] Tool use / Function calling

* [ ] ReAct

* [ ] Memory, планирование

* [ ] MCP — базово

  

### Evaluation & Safety

  

* [ ] Бенчмарки (MMLU и т.п.) и их ограничения

* [ ] LLM-as-a-judge

* [ ] ⭐ Hallucinations: причины и способы снижения

* [ ] Prompt injection, jailbreaks

* [ ] Multimodal LLM (VLM) — базово

  

---

  

# 26. RAG

  

### Основы

  

* [ ] ⭐ Зачем RAG, RAG vs Fine-tuning

* [ ] ⭐ Пайплайн: ingestion → chunking → embedding → indexing → retrieval → reranking → generation

  

### Indexing

  

* [ ] Парсинг документов (PDF, таблицы, HTML)

* [ ] ⭐ Chunking: fixed-size, recursive, semantic, overlap, размер чанка

* [ ] Metadata

* [ ] Embedding models, выбор модели

  

### Retrieval

  

* [ ] Similarity: cosine, dot product, L2

* [ ] ⭐ Sparse (BM25) vs Dense retrieval

* [ ] ⭐ Hybrid search, Reciprocal Rank Fusion

* [ ] ⭐ Bi-encoder vs Cross-encoder, reranking

* [ ] Vector DB: FAISS, Qdrant, Milvus, pgvector

* [ ] ANN-индексы: ⭐ HNSW, IVF, PQ

* [ ] Metadata filtering

  

### Query & Context

  

* [ ] Query rewriting, multi-query, HyDE

* [ ] Lost in the middle

* [ ] Context compression

* [ ] Цитирование источников

  

### Evaluation

  

* [ ] Retrieval: Recall@K, MRR, NDCG

* [ ] Generation: faithfulness, answer relevance

* [ ] Context precision / recall, RAGAS

* [ ] Построение eval-датасета

  

### Advanced

  

* [ ] Agentic RAG

* [ ] Multi-hop RAG

* [ ] GraphRAG — идея

* [ ] Failure modes: плохой retrieval vs плохая генерация — как диагностировать

* [ ] Кеширование, latency, стоимость

  

---

  

# Часть IV. Engineering & Production

  

# 27. Python, SQL, алгоритмы

  

### Python

  

* [x] NumPy

* [ ] Pandas: groupby, merge, apply, pivot, векторизация

* [ ] Python data structures

* [ ] Генераторы, итераторы, декораторы, контекстные менеджеры

* [ ] Mutable / immutable, копирование

* [ ] GIL, multiprocessing vs threading — базово

  

### SQL

  

* [ ] JOIN (все виды)

* [ ] GROUP BY, HAVING

* [ ] Window functions

* [ ] CTE

* [ ] Subqueries

* [ ] NULL — подводные камни

  

### Algorithms

  

* [x] Big O

* [x] Hash table

* [x] List

* [x] Stack / Queue

* [x] Sorting

* [x] Binary Search

* [ ] Two pointers, sliding window

* [ ] Heap

* [ ] Graphs: BFS / DFS

* [ ] Trees, рекурсия

* [ ] Dynamic programming — базово

  

---

  

# 28. MLOps

  

* [ ] ML Pipeline

* [ ] Experiment tracking: MLflow / W&B

* [ ] Версионирование данных и моделей (DVC)

* [ ] Reproducibility: seeds, окружения

* [ ] Docker

* [ ] Model serving: FastAPI, Triton

* [ ] Экспорт моделей: ONNX, TorchScript

* [ ] Batch vs online inference

* [ ] Monitoring

* [ ] CI/CD для ML

* [ ] Распределённое обучение: DDP, FSDP — базово

  

---

  

# 29. ML System Design

  

* [ ] ⭐ Схема ответа: бизнес-цель → ML-задача → данные → baseline → модель → метрики → деплой → мониторинг

* [ ] Постановка ML-задачи

* [ ] Target

* [ ] Features

* [ ] Training pipeline

* [ ] Offline / online features

* [ ] Batch inference

* [ ] Online inference

* [ ] Model serving

* [ ] Latency

* [ ] Throughput

* [ ] Scalability

* [ ] Monitoring

* [ ] Data drift

* [ ] Concept drift

* [ ] Retraining

* [ ] Offline vs online метрики

* [ ] Cold start

* [ ] Feedback loops

* [ ] Feature Store

* [ ] Model Registry

  

### Типовые кейсы

  

* [ ] Рекомендательная система / лента

* [ ] Поиск и ранжирование

* [ ] Антифрод / модерация объявлений

* [ ] Прогноз спроса / цены

* [ ] LLM-ассистент / RAG-система для поддержки

  

---

  

# 30. A/B Testing

  

* [ ] Гипотезы

* [ ] Метрики: целевые, прокси, guardrail

* [ ] p-value

* [ ] Доверительный интервал

* [ ] Статистическая значимость

* [ ] Практическая значимость

* [ ] MDE

* [ ] Размер выборки

* [ ] Multiple testing

* [ ] CUPED — базово

* [ ] Peeking problem

* [ ] Network effects, sample ratio mismatch

  

---

  

# 31. Практические задачи

  

### Classical ML

  

* [ ] написать Linear Regression на NumPy

* [ ] написать Logistic Regression

* [ ] реализовать Gradient Descent

* [ ] реализовать K-Means

* [ ] реализовать Decision Tree (split по Gini)

* [ ] реализовать metrics (ROC-AUC, F1, NDCG)

* [ ] написать train/validation pipeline

* [ ] найти leakage в коде

* [ ] объяснить, почему модель переобучилась

* [ ] выбрать metric под бизнес-задачу

* [ ] подобрать threshold

* [ ] разобрать confusion matrix

* [ ] объяснить feature importance

* [ ] разобрать плохой эксперимент

  

### Deep Learning

  

* [ ] написать training loop на PyTorch

* [ ] реализовать backprop для MLP на NumPy

* [ ] реализовать self-attention / multi-head attention

* [ ] fine-tune BERT на классификацию

* [ ] LoRA fine-tuning небольшой LLM

* [ ] собрать простой RAG (chunking + embeddings + FAISS + LLM) и оценить его

  

### Coding

  

* [ ] SQL-задачи

* [ ] Python-задачи

* [ ] Big-O задачи

* [ ] ML case questions

  

---

  

# Частые вопросы на собеседовании

  

* [ ] Bias-variance tradeoff — объяснить на примере

* [ ] Почему L1 даёт разреженность, а L2 — нет

* [ ] Как работает градиентный бустинг, чем отличается от RF

* [ ] Что такое ROC-AUC и как его посчитать руками

* [ ] Что делать при дисбалансе классов

* [ ] Как бороться с переобучением (в ML и в DL)

* [ ] Откуда берётся log-loss (MLE)

* [ ] Как найти и предотвратить data leakage

* [ ] Vanishing gradients: причины и решения

* [ ] BatchNorm vs LayerNorm

* [ ] Как работает attention, зачем √d, сложность

* [ ] Чем BERT отличается от GPT

* [ ] Что такое KV-cache и зачем он нужен

* [ ] LoRA: как работает и почему экономит память

* [ ] Как устроен RAG и как оценить его качество

* [ ] Как снизить галлюцинации LLM

* [ ] Модель хорошо работает offline, но плохо в проде — почему?

* [ ] Как задизайнить рекомендации / поиск для маркетплейса