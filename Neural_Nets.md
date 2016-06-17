# Нейронные сети

[TOC]

---

### Нейроны

---

#### Целевая функция

Целевая функция должна удовлетворять 3 условия:

1. Дифференцируемость

1. Зависимость от выходов сети

1. Производная целевой функции должна выражаться как сумма производных по  отдельным примерам

Виды целевых функций:

1. Квадратичная
$$
J = \frac{1}{2n}\sum^n_{i=1}(\hat y^{(i)} - y^{(i)})^2
$$

1. Cross-entropy loss
$$
J = -\frac{1}{n}\sum^n_{i=1}(y^{(i)}\ ln\ \hat y^{(i)} + (1-y^{(i)})\ ln(1-\hat y^{(i)}))
$$

1. SoftMax - позволяет получить вероятности при категориальном анализе

---

#### Регуляризация

Регуляризация призвана не допусть слишком больших значений весов путём штрафования за величину каждого отдельного веса.
$\lambda$ - константа штрафования за вес

Виды регуляризации:

1. L2
$$
J_{L2} = J_0 + \lambda_2 \sum^L_{l=1}\sum^J_{j=1}\sum^K_{k=1}(w_{jk}^l)^2
$$
$$
\frac{\delta J_{L2}}{\delta w_{jk}^l} = \frac{\delta J_0}{\delta w_{jk}^l} + \lambda_2 w_{jk}^l
$$

1. L1
$$
J_{L1} = J_0 + \lambda_1 \sum^L_{l=1}\sum^J_{j=1}\sum^K_{k=1}|w_{jk}^l|
$$
$$
\frac{\delta J_{L1}}{\delta w_{jk}^l} = \frac{\delta J_0}{\delta w_{jk}^l} + \lambda_1 sign(w_{jk}^l)
$$
$$
sign(w_{jk}^l) = \begin{cases}
1, & если w_{jk}^l > 0 \\
0, & если w_{jk}^l = 0 \\
-1, & если w_{jk}^l < 0
\end{cases}
$$

1. Elastic net

---

#### Перцептрон

На входе перцептрон получает булевы значения типа (1,0,1,1,0). Внутри имеет веса для каждого из значений. Суммирует произведения булевых значений на веса. Если эта сумма выше порога - возвращает 1, если ниже - возвращает 0.

\begin{equation}
f(\textbf{x}, \textbf{w}, b) = 
  \begin{cases}
    1,  \quad если   \displaystyle\sum_{i=1}^m w_{i} x_{i} + b > 0       \\\
    0,  \quad иначе
  \end{cases}
\end{equation}

Пример:
Дана таблица с наблюдениями

\begin{pmatrix}
  желтизна & симметричность & это-груша? \\\
  \dots & \dots & \dots \\\
  1 & 0.3 & да \\\
  0,4  & 0,5 & да \\\
  0,7 & 0.8 & да 
\end{pmatrix}

Решение:

```python
#!/usr/bin/env python3.5
import numpy as np


W = np.array([0, 0, 0])
DATA = (
    np.array((1  , 1  , 0.3, 1)),
    np.array((1  , 0.4, 0.5, 1)),
    np.array((1  , 0.7, 0.8, 0))
)


def predict(w, data): # если умножение векторов даёт положительную величину - возвращаем 1, иначе 0
    weights = np.array(w)
    if weights @ data > 0:
        return 1
    else:
        return 0


perfect = False # предполагаем, что веса не идеальны
while not perfect:
    perfect = True # даём нашим весам шанс показать, что они идеальны
    for case in DATA: # тестируем каждое известное вхождение данных
        result = case[-1]
        prediction = predict(W, case[:-1])
        if prediction != result: # если хотя бы один из примеров не проходит тест
            perfect = False # говорим, что веса не идеальны
            if prediction == 0:
                W = W + case[:-1]
            else:
                W = W - case[:-1]


print(W)
# >>> [ 1.   1.6 -3.1]
```

---

#### Линейный нейрон

Логика та же, что и у перцептрона, однако возвращаем не булево значение, а скалярное произведение векторов весов и переменных.

$$
f(\textbf{x}, \textbf{w}, b) = \sum_{i=1}^m w_{i} x_{i} + b
$$

или в случае использования линейной алгебры (когда в весах первым элементов добавляется w<sub>0</sub>=0, а во всех рядах переменных x<sub>0</sub>=1)

$$
f(\textbf{x}, \textbf{w}) = \textbf{x} \times \textbf{w}
$$

---

#### Сигмоидальный (логистический) нейрон

Аналогично перцептрону возвращаемые значения стремятся к 0 или 1, однако переход от 0 к 1 плавный

$$
f(\textbf{x}, \textbf{w}, b) = \sigma(\textbf{x} \times \textbf{w} + b)
$$

где

$$
\sigma(x) = \frac{1}{1 + e^{-x}}
$$

$$
\sigma '(x) = \sigma (x) - \sigma^2 (x)
$$

---

#### Гиперболический тангенс

Аналогичен сигмоидальному нейрону, но значения колеблятся от -1 до 1, при этом кривая проходит через начало координат.

$$
f(\textbf{x}, \textbf{w}, b) = tanh(\textbf{x} \times \textbf{w} + b)
$$

где

$$
tahn(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}}
$$

Отношение сигмы и гиперболического тангенса:

$$
tanh(x) = \sigma(2x) - \sigma(-2x)
$$

---

#### Rectified linear unit (ReLU)

Логика похожа на логику линейного нейрона, однако возвращает 0 в случае, когда результат меньше ноля.

$$
f(\textbf{x}, \textbf{w}, b) = max(\textbf{x} \times \textbf{w} + b, 0)
$$

---

#### Softplus

Похожа по форме на ReLU , однако является дифференцируемой

$$
softplus(\textbf{x}, \textbf{w}, b) = ln(1 + e^{\textbf{x} \times \textbf{w} + b})
$$

Производная от функции softplus(x):

$$
softplus'(x) = \sigma(x)
$$

---

#### Алгоритм применения стохастического градиентного спуска

1. Случайным образом выбираем часть примеров из всех имеющихся

1. Считаем  $\hat{y}$ для каждого из них

1. Вычисляем градиент целевой функции по весам для каждого из них

1. Суммируем то, что получилось

1. Обновляем веса

1. Проверяем критерии остановки алгоритма. Если хотя бы один из них отработал - выходим из цикла

---

#### Регрессия + Линейный нейрон

$\nabla J$ - градиент в конкретной точке

$$
\nabla J = \frac{1}{n}\sum_{i=1}^{n}
  \begin{bmatrix}
    \frac{\partial J}{\partial w_1} \\\
    \dots \\\
    \frac{\partial J}{\partial w_m}
  \end{bmatrix}
 = \frac{1}{n}\sum_{i=1}^{n}
  \begin{bmatrix}
    (\hat{y}^{(i)} - y^{(i)})x_0^{(i)} \\\
    \dots \\\
    (\hat{y}^{(i)} - y^{(i)})x_j^{(i)} \\\
    \dots \\\
    (\hat{y}^{(i)} - y^{(i)})x_m^{(i)}
  \end{bmatrix}
$$

---

#### Регрессия + Сигмоидальный нейрон

$$
\nabla J = \frac{1}{n}\sum_{i=1}^{n}
  \begin{bmatrix}
    \frac{\partial J}{\partial w_1} \\\
    \dots \\\
    \frac{\partial J}{\partial w_m}
  \end{bmatrix}
 = \frac{1}{n}\sum_{i=1}^{n}
  \begin{bmatrix}
    \dots \\\
    (\hat{y}^{(i)} - y^{(i)})x_j^{(i)} \\\
    \dots
  \end{bmatrix}
 = \frac{1}{n}\sum_{i=1}^{n}
  \begin{bmatrix}
    (\sigma(w^T x^{(i)}) - y^{(i)})(\sigma(w^T x^{(i)}) - \sigma^2(w^T x^{(i)}))x_0^{(i)} \\\
    \dots \\\
    (\sigma(w^T x^{(i)}) - y^{(i)})(\sigma(w^T x^{(i)}) - \sigma^2(w^T x^{(i)}))x_j^{(i)} \\\
    \dots \\\
    (\sigma(w^T x^{(i)}) - y^{(i)})(\sigma(w^T x^{(i)}) - \sigma^2(w^T x^{(i)}))x_m^{(i)}
  \end{bmatrix}
$$

*Алгоритм рассчёта:*

1. Получаем вертикальный вектор $\hat y$ (предсказания по всем примерам при нынешних весах). Размер (n,1)
1. Получаем вертикальный вектор $\delta$. Это разница между $\hat y$ и реальными значениями $y$. Размер (n,1)
1. Получаем матрицу $derivative\_by\_weight$ того же размера, что и матрица данных $X$. Для этого матрицу $X$ умножаем построчно на соответствующий элемент из вектора $\delta$ и умножаем на соответствующий элемент из вектора $y\_derivative$ (равный $\hat y - \hat y^2$)
1. Получаем горизонтальный вектор градиента путём нахождения средних значений по столбцам
1. Транспонируем горизонтальный вектор. На выходе получили вертикальный вектор градиента. Можно вычетать его произведение с костантой обучения из вектора весов.

Пример:
```python
prediction = self.activation()
delta_y = prediction - y
derivative_by_weights = X * delta_y * self.activation_derivative()
gradient = derivative_by_weights.mean(axis=0)[:, np.newaxis]
```

---

### Многослойные нейронные сети

***"Перцептрон Румельхарта"***
![Multilayer Perceptron](/home/vasyl/docs/img/multilayer_perceptron.jpg)

Нотация веса входящей связи между нейронами: $w_{jk}^{l}$ , где:

1. $l$ - слой нейрона, в который входит информация
1. $j$ - индекс нейрона, в который входит информация
1. $k$ - индекс нейрона, из которого выходит информация (у которого слой имеет номер $l-1$)

$W^l = [нейроны\_l \times нейроны\_l-1]$ - матрица весов входящих связей для всего слоя.

Нотация результата сумматорной функции нейрона: $Z_j^l$ , где:

1. $l$ - слой нейрона
1. $j$ - индекс нейрона

Нотация результата активационной функции нейрона: $a_j^l$ , где:

1. $l$ - слой нейрона
1. $j$ - индекс нейрона

Нотация вектора смещений конкретного слоя нейронов: $b^l$ , где:

1. $l$ - слой нейрона

Формула активационной функции для сигмоидального нейрона:

$$
a_j^l = \sigma (\sum_k w_{jk}^{l}a_j^{l-1} + b^l_j)
$$

Формула вектора активационной функции для линейных нейронов слоя $l$ в зависимости от слоя $l-2$ , где $a()$ - активационная функция, одинаковая для всех нейронов:

$$
a^l = a(W^l a(W^{l-1} a^{l-2} + b^{l-1}) + b^l)\\
или\\
a^l = a(W^l a^{l-1} + b^l) , где\ a^{l-1} = a(W^{l-1} a^{l-2} + b^{l-1})
$$

Целевая функция для работы нейронов при множественном (не бинарном) выборе:

$$
J = \frac{1}{2n}\sum_{i=1}^{n}\sum_{j=1}^{K}(y_j^{(i)} - \hat y_j^{(i)})^2
$$

где $K$ - количество классификаторов (ie вариантов ответа)
Вектор $K$ - кодирование по принципу *one hot encoding* , то-есть это вектор из нулей с единственной единицей (где единица обозначает правильный ответ)

---

#### Ошибка нейрона

Ошибка нейрона - это частная производная целевой функции по сумматорной функции нейрона:

$$
\delta_j^l = \frac{\delta J}{\delta z_j^l}
$$

Ошибка нейрона с номером $j$ из выходного слоя. Тип нейрона — сигмоидальный.

$$
\delta^L_j = \sigma(z_j)(\sigma(z_j)-y_j)(1-\sigma(z_j))
$$

Вектор ошибок нейронов из выходного слоя. Тип нейронов — сигмоидальный.

$$
\delta^L = \sigma(z^L)\odot(\sigma(z^L)-y)\odot(1-\sigma(z^L))
$$

Вектор ошибок слоя $l$:

$$
\delta^l = ((w^{l+1})^T \delta^{l+1}) \odot \sigma^{'}(z^l) 
$$

Пример решения:

```python
deltas = np.array([[0.3, 0.2], [0.3, 0.2]]) # (пример, нейрон)
sums = np.array([[0, 1, 1], [0, 2, 2]]) # (пример, нейрон)
weights = np.array([[0.7, 0.2, 0.7], [0.8, 0.3, 0.6]]) # (нейрон[l+1], нейрон[l])

# пример решения влоб, подсчиитывая ошибку перебором по каждому примеру
# отдельно и потом находя среднюю
deltas_0 = []
for i in range(deltas.shape[0]):
    deltas_0.append((deltas[i] @ weights)[:, np.newaxis] * sigmoid_prime(sums[i][:, np.newaxis]))
print(np.array(deltas_0).mean(axis=0))

# пример решения матричным способом. Результат тот же
print(((deltas @ weights) * sigmoid_prime(sums)).mean(axis=0))
```

---

#### Алгоритм обновления весов и смещений

1. Осуществить прямое распространение активации для каждого примера

1. Находим ошибки нейронов выходного слоя
$$
\delta^L = \nabla_a J \odot \sigma^{'}(z^L)
$$

1. Находим ошибки нейронов скрытых слоёв
$$
\delta^l = \Big((W^{l+1})^T  \delta^{l+1}\Big) \odot \sigma^{'}(z^L)
$$

1. Находим градиент смещения в каждом слое
$$
\frac{\delta J}{\delta b^l_j} = 
\delta^l_j
$$

1. Находим градиент весов в каждом слое
$$
\frac{\delta J}{\delta w^l_{jk}} = a^{l-1}_k
\delta^l_j
$$

1. Обновляем параметры

1. Проверяем критерии остановки алгоритма

---