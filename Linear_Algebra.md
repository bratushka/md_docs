# Линейная алгебра

[TOC]

---

### Понятие матрицы

Матрицей называется прямоугольная таблица чисел, например:
```
    | 1.2  -5.3  10.2|
    |-8.2  15.9   5.0|
X = | 1.4  47.5   1.8|
    | 7.0   8.7  12.6|
    | 5.1   7.5   1.9|
```

Матрицы обозначаются заглавными полужирными буквами (**A**), а их элементы — соответствующими строчными буквами с индексами, т.е. a<sub>ij</sub>. Первый индекс нумерует строки, а второй — столбцы.

Пара чисел I и J называется размерностью матрицы и обознается как I×J.

Квадратная единичная матрица (нулевая матрица с еденицами по диагонали из левого верхнего угла в противоположный) называется **I**. Например:
```
    |1 0 0|
I = |0 1 0|
    |0 0 1|
```

Матрица называется диагональной, если все ее элементы, кроме диагональных (a<sub>ii</sub>) равны нулю. Например:
```
    |1 0 0|
X = |0 2 0|
    |0 0 5|
```

Матрица называется верхней треугольной, если все ее элементы, лежащие ниже диагонали, равны нулю, т.е. a<sub>ij</sub> = 0, при i>j. Например:
```
    |1 4 6|
X = |0 2 9|
    |0 0 5|
```
Аналогично определяется и нижняя треугольная матрица.

Матрица A называется симметричной, если **A<sup>t</sup> = A**. Иными словами a<sub>ij</sub> = a<sub>ji</sub>.

Матрица A называется ортогональной, если **A<sup>t</sup>A = AA<sup>t</sup> = I.**

Матрица называется нормальной если **A<sup>t</sup>A = AA<sup>t</sup>**

---

### Понятие вектора

Если матрица состоит только из одного столбца (J = 1), то такой объект называется вектором. Точнее говоря, вектором-столбцом. Можно рассматривать и матрицы, состоящие из одной строки. Например:
```
    | 1.2 |
    |-8.2 |
x = | 1.4 |
    | 7.0 |
    | 5.1 |

y = | 1.4  47.5   1.8|
```

---

### Простейшие операции с матрицами

1. Матрицы можно умножать на числа. При этом каждый элемент умножается на это число.

1. Две матрицы одинаковой размерности можно поэлементно складывать и вычитать.

1. Матрицу можно транспонировать. При этой операции матрица переворачивается, т.е. строки и столбцы меняются местами. Транспонирование обозначается штрихом, A' или индексом A<sup>t</sup>.

---

### Умножение матриц

\begin{equation}
c_{ij} = \sum_{k=1}^K a_{ik} b_{kj}
\end{equation}

Матрицы можно перемножать, но только в том случае, когда они имеют соответствующие размерности. Почему это так, будет ясно из определения. Произведением матрицы A, размерностью I×K, и матрицы B, размерностью K×J, называется матрица C, размерностью I×J, элементами которой являются числа.

Количество операций для умножения двух матриц равно i * k * j

Свойства умножения:

1. **AB ≠ BA**

1. **ABC = (AB)C = A(BC)**

1. **A(B+C) = AB+AC**

---

### Поиск коэффициентов линейной регрессии

Формула регрессии

\begin{equation}
y = b_{0} + b_{1}x_{1} + b_{2}x_{2} + ... + b_{m}x_{m}
\end{equation}

Вектор значений коэффициентов **b** = (X<sup>t</sup> @ X)<sup>-1</sup> @ X<sup>t</sup> @ y

Пример:
Имеем наблюдения:

| D   | V   |
|:---:|:---:|
| 10  | 60  |
|  7  | 50  |
| 12  | 75  |

Необходимо найти зависимость D от V
Итак матрица значений **X** будет состоять из столбца с еденицами и столбцов значений переменных (в нашем случае столбца V)
```
    |1 60|
X = |1 50|
    |1 75|
```

Значения вектора **y** будут равны значениям столбца D (предсказуемых значений)
```
    |10|
y = | 7|
    |12|
```

Считаем **b**
```python
import numpy as np
X = np.array([[1, 60], [1, 50], [1, 75]])
y = np.array([10, 7, 12])

b = np.linalg.inv(X.T @ X) @ X.T @ y
# или для Python < 3.5
b = np.linalg.inv(X.T.dot(X)).dot(X.T).dot(y)
```

На выходе получили
```
b = |-2.34210526 |
    | 0.19473684 |
```

Итак формула линейной регрессии D на V
$$
d = -2.34210526 + 0.19473684v
$$
