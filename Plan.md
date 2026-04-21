# План подготовки: 3-4 дня × 12 часов

Исходные данные: сильная база в программировании и DL/CV, слабые места — Python-синтаксис, алгоритмы, классический ML. Строим план от критичного к второстепенному.

---

## День 1 — Python Core (12 часов)

**Цель: закрыть все "питонические" темы, которые спрашивают в лоб**

### Блок 1: Генераторы и итераторы (2.5 часа)

**Читай:** [Real Python — Generators](https://realpython.com/introduction-to-python-generators/)

Что понять и написать руками:

```python
# 1. Разница: list comprehension vs generator expression
result = [x**2 for x in range(10)]   # список в памяти
result = (x**2 for x in range(10))   # объект-генератор

# 2. yield — написать самому
def fibonacci():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

# 3. Задача Ozon: читать 10GB файл строками
def read_large_file(filepath):
    with open(filepath) as f:
        for line in f:
            yield line.strip()

# 4. yield from
def chain(*iterables):
    for it in iterables:
        yield from it
```

**Задача для практики:** написать генератор, который читает файл и возвращает топ-10 слов по частоте. Решить без `readlines()`.

---

### Блок 2: Декораторы (2.5 часа)

**Читай:** [Real Python — Decorators](https://realpython.com/primer-on-python-decorators/)

```python
import functools
import time

# 1. Базовый декоратор
def my_decorator(func):
    @functools.wraps(func)  # сохраняет __name__, __doc__
    def wrapper(*args, **kwargs):
        print("До вызова")
        result = func(*args, **kwargs)
        print("После вызова")
        return result
    return wrapper

# 2. Декоратор с параметрами (часто спрашивают)
def retry(max_attempts=3, delay=1.0):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_attempts - 1:
                        raise
                    time.sleep(delay)
        return wrapper
    return decorator

# 3. Декоратор-класс (редко, но бывает)
class rate_limit:
    def __init__(self, max_calls, period):
        self.max_calls = max_calls
        self.period = period
        self.calls = []
    
    def __call__(self, func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            now = time.time()
            self.calls = [c for c in self.calls if now - c < self.period]
            if len(self.calls) >= self.max_calls:
                raise Exception("Rate limit exceeded")
            self.calls.append(now)
            return func(*args, **kwargs)
        return wrapper
```

**Написать самостоятельно:** декоратор `@cache` (аналог `lru_cache`), декоратор `@timer`, декоратор `@retry`.

---

### Блок 3: GIL и конкурентность (2.5 часа)

**Читай:** [Real Python — GIL](https://realpython.com/python-gil/)

**Главная схема в голове:**

```
Задача CPU-bound (матрицы, расчёты)?
  → multiprocessing (обходит GIL, отдельные процессы)

Задача I/O-bound (сеть, файлы, БД)?
  → asyncio (один поток, event loop)
  → threading (несколько потоков, GIL освобождается при I/O)
```

```python
# Threading — I/O задачи
import threading

def download(url):
    # GIL освобождается во время сетевого вызова
    pass

threads = [threading.Thread(target=download, args=(url,)) for url in urls]
for t in threads: t.start()
for t in threads: t.join()

# Asyncio — современный способ
import asyncio

async def fetch(url):
    await asyncio.sleep(1)  # неблокирующее ожидание
    return url

async def main():
    results = await asyncio.gather(*[fetch(url) for url in urls])

asyncio.run(main())

# Multiprocessing — CPU задачи
from multiprocessing import Pool

with Pool(4) as p:
    results = p.map(heavy_computation, data_list)
```

**Вопросы, которые задают:**

- Что такое GIL? Почему он есть? (CPython, reference counting, thread safety)
- Как обойти GIL для CPU-bound задач?
- `asyncio.gather` vs `asyncio.wait` — разница?
- Что такое race condition? Как защититься? (Lock, Semaphore)

---

### Блок 4: ООП и магические методы (2 часа)

```python
# Самые часто спрашиваемые
class MyClass:
    def __init__(self):        # конструктор
    def __repr__(self):        # repr(obj) — для дебага
    def __str__(self):         # str(obj) — для вывода
    def __len__(self):         # len(obj)
    def __getitem__(self, key): # obj[key]
    def __contains__(self, item): # item in obj
    def __enter__(self):       # with obj:
    def __exit__(self, *args): # выход из with

# MRO (Method Resolution Order) — порядок поиска метода
class A: pass
class B(A): pass
class C(A): pass
class D(B, C): pass
print(D.__mro__)  # D -> B -> C -> A -> object
```

**Типичный вопрос:** _"Что выведет этот код?"_

```python
# Ловушка с mutable default argument
def append_to(element, to=[]):
    to.append(element)
    return to

print(append_to(1))  # [1]
print(append_to(2))  # [1, 2] — НЕ [2] !
```

---

### Блок 5: Практика — пиши код (2.5 часа)

Открой [solvit.space/coding?company_ids=55](https://solvit.space/coding?company_ids=55) — задачи Ozon:

- Декоратор повторения
- Самый длинный палиндром
- Найти впадину (local minimum)
- Move Zeroes

**Правило:** пиши в текстовом редакторе без автодополнения, потом запускай.

---

## День 2 — Алгоритмы + практика (12 часов)

### Блок 1: Big-O и базовые структуры (1.5 часа)

Выучить наизусть эту таблицу:

|Структура|Access|Search|Insert|Delete|
|---|---|---|---|---|
|Array/List|O(1)|O(n)|O(n)|O(n)|
|Dict/Set|—|O(1) avg|O(1) avg|O(1) avg|
|Deque|O(n)|O(n)|O(1) ends|O(1) ends|
|Heap|—|O(n)|O(log n)|O(log n)|

---

### Блок 2: Два указателя + Sliding Window (2 часа)

```python
# Two pointers — palindrome check
def is_palindrome(s):
    left, right = 0, len(s) - 1
    while left < right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
    return True

# Sliding window — longest substring without repeats
def length_of_longest_substring(s):
    seen = {}
    left = max_len = 0
    for right, char in enumerate(s):
        if char in seen and seen[char] >= left:
            left = seen[char] + 1
        seen[char] = right
        max_len = max(max_len, right - left + 1)
    return max_len
```

**Задачи (NeetCode):** Move Zeroes, Valid Palindrome, Container With Most Water, Longest Substring Without Repeats

---

### Блок 3: Бинарный поиск (1.5 часа)

```python
def binary_search(nums, target):
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = left + (right - left) // 2  # не (l+r)//2 — overflow!
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

**Задачи:** Search in Rotated Sorted Array, Find First and Last Position

---

### Блок 4: Сортировки — только понять принцип (1 час)

Не реализовывать все с нуля. Знать:

- **Merge sort**: O(n log n), stable, extra O(n) memory — рекурсивно делим пополам, сливаем
- **Quick sort**: O(n log n) avg, O(n²) worst, in-place — pivot, partition, рекурсия
- **Heap sort**: O(n log n), in-place, нестабильный — строим кучу, извлекаем max

Уметь объяснить словами, не писать с нуля.

---

### Блок 5: Стек + Хэш-таблица (1.5 часа)

```python
# Balanced brackets — классика
def is_valid(s):
    stack = []
    mapping = {')': '(', '}': '{', ']': '['}
    for char in s:
        if char in mapping:
            top = stack.pop() if stack else '#'
            if mapping[char] != top:
                return False
        else:
            stack.append(char)
    return not stack

# Top-K frequent elements
from collections import Counter
import heapq

def top_k_frequent(nums, k):
    count = Counter(nums)
    return heapq.nlargest(k, count.keys(), key=count.get)
```

---

### Блок 6: Практика — 4 задачи на время (4 часа)

Каждой задаче — 45 минут максимум. Без подсказок, в текстовом редакторе:

1. Group Anagrams (LC 49)
2. Valid Parentheses (LC 20)
3. Find Peak Element (LC 162) — "найти впадину"
4. Power of Two (LC 231)

После каждой: разбор edge cases (пустой массив, один элемент, отрицательные числа).

---

## День 3 — Классический ML + CV (12 часов)

### Блок 1: Классический ML — экспресс (3 часа)

**Линейные модели:**

- Linear Regression: MSE loss, нормальное уравнение vs градиентный спуск
- Logistic Regression: BCE loss, sigmoid, вероятности, не классификатор напрямую
- L1 (Lasso) обнуляет веса → feature selection; L2 (Ridge) уменьшает веса → не обнуляет

**Деревья и бустинг:**

- Decision Tree: Gini impurity vs Entropy для сплита, склонен к переобучению
- Random Forest: bagging + feature subsampling, уменьшает variance
- Gradient Boosting (XGBoost/CatBoost/LightGBM): ансамбль слабых деревьев, каждое следующее исправляет ошибки предыдущего, уменьшает bias

**Метрики — знать когда что:**

- Accuracy: бесполезна при дисбалансе классов
- Precision/Recall/F1: при дисбалансе
- ROC-AUC: ранжирование, инвариантна к порогу и монотонным преобразованиям
- PR-AUC: лучше ROC-AUC при сильном дисбалансе

**Кластеризация:**

- K-Means: минимизирует inertia, чувствителен к выбросам и инициализации
- DBSCAN: не нужно знать k, находит произвольные формы, выбросы → шум
- Метрики: Silhouette score, Davies-Bouldin

**Вопросы, которые задают:**

- Как работает gradient boosting? Чем отличается от bagging?
- Когда L1, когда L2?
- ROC-AUC 0.5 — что это значит?
- Как бороться с дисбалансом классов?

---

### Блок 2: Детекция — R-CNN family + YOLO (3 часа)

У тебя есть опыт с YOLO, поэтому акцент на теорию и сравнение:

**Путь эволюции:**

```
R-CNN (2014):
  → Selective Search → 2000 proposals
  → Каждый proposal через CNN отдельно
  → SVM для классификации, регрессия bbox
  → МЕДЛЕННО: ~47 секунд/изображение

Fast R-CNN:
  → Всё изображение через CNN один раз
  → RoI Pooling: проецируем proposals на feature map
  → Общая feature map → быстрее

Faster R-CNN:
  → RPN (Region Proposal Network) вместо Selective Search
  → Anchor boxes: несколько масштабов/соотношений
  → RoI Align вместо RoI Pooling (нет квантизации)
  → Лосс: cls + bbox_reg + rpn_cls + rpn_reg

YOLO (you know):
  → One-stage: нет отдельного proposal step
  → Grid cells → напрямую bbox + class
  → Намного быстрее, чуть хуже precision
```

**Ключевые концепции:**

- **NMS (Non-Maximum Suppression):** убирает дубликаты bbox. Порог IoU → если перекрытие > threshold, оставляем только с максимальным confidence
- **mAP@0.5:** для каждого класса считаем AP (area under PR curve при IoU≥0.5), усредняем по классам
- **Anchor boxes:** pre-defined shapes разных размеров, сеть предсказывает offset от anchor
- **FPN (Feature Pyramid Network):** предсказываем на разных масштабах feature maps → лучше детектим маленькие объекты

---

### Блок 3: Сегментация (2 часа)

```
Semantic segmentation:
  → Каждый пиксель → класс
  → U-Net: encoder-decoder + skip connections
  → DeepLab: dilated convolutions + ASPP

Instance segmentation:
  → Каждый объект → отдельная маска
  → Mask R-CNN = Faster R-CNN + mask head
  → RoI Align критически важен (нет потери точности при проецировании)

Panoptic segmentation:
  → Semantic + Instance вместе
```

**U-Net** — уметь объяснить:

- Encoder (downsampling) + Decoder (upsampling)
- Skip connections: конкатенируем feature maps энкодера с декодером → сохраняем детали
- Применение: медицина, спутники, — где нужна точная локализация

**Метрики сегментации:**

- IoU (Jaccard): `intersection / union` — основная метрика
- Dice coefficient: `2*intersection / (pred + gt)` — популярна в медицине
- mIoU: усредняем IoU по всем классам

---

### Блок 4: CV Deep-dive — что ещё спросят (2 часа)

**Свёртки:**

- Обычная conv: большое ядро → много параметров
- Depthwise separable conv (MobileNet): depthwise + pointwise → в ~9× меньше параметров
- Dilated conv (атрозная): dilation rate > 1 → увеличивает receptive field без downsampling

**Калибровка камеры (специфика вакансии):**

```
Матрица камеры K:
  [fx  0  cx]
  [ 0 fy  cy]
  [ 0  0   1]

fx, fy — фокусное расстояние в пикселях
cx, cy — оптический центр

Дисторсия: k1, k2 (радиальная), p1, p2 (тангенциальная)
cv2.calibrateCamera() — шахматная доска → находим K и дисторсию
cv2.undistort() — исправляем изображение
```

**OpenCV — ключевые функции:**

```python
import cv2

img = cv2.imread('image.jpg')

# Предобработка
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
blurred = cv2.GaussianBlur(gray, (5, 5), 0)

# Детекция краёв
edges = cv2.Canny(blurred, 50, 150)

# Контуры — для измерения габаритов!
contours, _ = cv2.findContours(edges, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
for cnt in contours:
    x, y, w, h = cv2.boundingRect(cnt)  # ограничивающий прямоугольник
    rect = cv2.minAreaRect(cnt)          # повёрнутый прямоугольник
    box = cv2.boxPoints(rect)            # 4 точки угла

# Perspective transform (измерение реальных размеров)
M = cv2.getPerspectiveTransform(src_pts, dst_pts)
warped = cv2.warpPerspective(img, M, (width, height))
```

---

### Блок 5: Закрепление — вопросы вслух (2 часа)

Открой любой таймер, задай себе вопросы и отвечай вслух — имитируй собеседование:

- Объясни как работает Faster R-CNN. Чем отличается RoI Align от RoI Pooling?
- Как измерить реальный размер объекта по одной камере?
- Что такое FPN? Зачем он нужен?
- Gradient boosting vs Random Forest — когда что выбрать?

---

## День 4 — Закрепление + Mock Interview (12 часов)

### Блок 1: Повтор Python — слабые места (2 часа)

Пройди [yakimka/python_interview_questions](https://github.com/yakimka/python_interview_questions) — только разделы:

- Типы данных (изменяемые/неизменяемые)
- Функции (closure, nonlocal, lambda)
- ООП (MRO, dunder методы)
- Конкурентность (GIL, asyncio)

---

### Блок 2: Алго-тренировка — 5 задач за 3 часа

|Задача|LeetCode|Паттерн|
|---|---|---|
|Two Sum|LC 1|Hash map|
|Valid Parentheses|LC 20|Stack|
|Binary Search|LC 704|Binary search|
|Move Zeroes|LC 283|Two pointers|
|Top K Frequent Elements|LC 347|Heap + Counter|

Правило: 30 минут на задачу. Если не решил — пиши что успел, потом разбор.

---

### Блок 3: SQL — оконные функции (2 часа)

```sql
-- Нарастающий итог (cumulative sum)
SELECT 
    date,
    revenue,
    SUM(revenue) OVER (ORDER BY date) as cumulative_revenue
FROM sales;

-- LAG/LEAD — сравнение с предыдущей строкой
SELECT 
    date,
    revenue,
    LAG(revenue, 1) OVER (ORDER BY date) as prev_revenue,
    revenue - LAG(revenue, 1) OVER (ORDER BY date) as growth
FROM sales;

-- ROW_NUMBER vs RANK vs DENSE_RANK
SELECT 
    employee,
    salary,
    RANK() OVER (PARTITION BY department ORDER BY salary DESC) as rank
FROM employees;
```

**Практика:** [solvit.space Ozon SQL задачи](https://solvit.space/coding?company_ids=55) — 3-4 задачи с окнами.

---

### Блок 4: Mock Interview — самое важное (3 часа)

Симулируй собеседование. Таймер, нет подсказок, пишешь в редакторе:

**Раунд 1 (45 мин):**

- Напиши декоратор `@retry(attempts=3)` — 15 мин
- Напиши генератор для построчного чтения файла и подсчёта топ-слов — 20 мин
- Edge cases: что если файл пустой? что если одно слово встречается миллион раз? — 10 мин

**Раунд 2 (45 мин):**

- Объясни GIL, asyncio, multiprocessing — 15 мин
- Реши задачу: дан список координат bbox и confidence, напиши NMS — 30 мин

**Раунд 3 (45 мин):**

- Объясни Faster R-CNN от начала до конца — 20 мин
- Как бы ты спроектировал систему измерения габаритов товаров? — 25 мин

---

### Блок 5: Подготовка рассказа о себе (2 часа)

Оzon спрашивает о реальном опыте. Подготовь 3-минутный рассказ по каждому:

- XRayLab: архитектура, метрики, какие проблемы решал, что бы изменил
- LexRAG: зачем RAG, как выбирал чанкинг, какие проблемы с retrieval
- Kaggle chest X-ray: какие метрики, как боролся с дисбалансом

---

## Итоговые приоритеты

```
КРИТИЧНО (делай в первую очередь):
✅ Генераторы + декораторы — написать 5 примеров руками
✅ GIL / asyncio / multiprocessing — объяснить схему
✅ Faster R-CNN + YOLO — архитектура + ключевые компоненты
✅ 10 алго-задач на NeetCode Easy/Medium

ВАЖНО:
🔸 Калибровка камеры (специфика вакансии!)
🔸 U-Net + Mask R-CNN
🔸 Классический ML (boosting, метрики)
🔸 SQL оконные функции

БОНУС (если останется время):
⚡ MRO, дескрипторы, metaclass
⚡ Стерео-зрение основы
⚡ pytest fixtures
```

