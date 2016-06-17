# Numpy
<a id="TOC"><a/>

[TOC]

---

### np.array

`class ndarray(builtins.object)`
```python
ndarray(shape, dtype=float, buffer=None, offset=0, strides=None, order=None)
```

*An array object represents a multidimensional, homogeneous array of fixed-size items.  An associated data-type object describes the format of each element in the array (its byte-order, how many bytes it occupies in memory, whether it is an integer, a floating point number, or something else, etc.)*

Constructing:
```python
np.array(object) # n-мерный массив из любой (возможно, вложенной) последовательности,
np.eye(N, M=N, k=0) # двумерный массив с N строками с единицами на диагонали и нулями во всех остальных позициях. Число столбцов M по умолчанию равно N, k — сдвиг диагонали (0 для основной диагонали, положительные числа для верхних диагоналей и отрицательные для нижних),
np.zeros(shape) # новый массив указанной формы, заполненный нулями,
np.ones(shape) # новый массив указанной формы, заполненный единицами,
np.full(shape, fill_value) # новый массив указанной формы, заполненный fill_value.

np.fromiter(iterator) # создаёт NumPy-массив из итератора, то есть заставляет итератор вычислить все доступные значения и сохраняет их в массив
np.loadtxt(fname, dtype=<type 'float'>, comments='#', delimiter=None, converters=None, skiprows=0, usecols=None, unpack=False, ndmin=0) # чтение из файла
np.hstack((array1, array2, ...)) # склеивает по строкам массивы, являющиеся компонентами кортежа, поданного на вход; массивы должны совпадать по всем измерениям, кроме второго
np.ones_like(array) # создаёт массив, состоящий из единиц, идентичный по форме массиву array
```

Selecting subarray or value:
```python
q = np.array((((1,2,3), (4,5,6), (7,8,9)), ((1,2,3), (4,5,6), (7,8,9))))

# a[..., 1] == a[:, 1]

# print(q)
[[[1 2 3]
  [4 5 6]
  [7 8 9]]

 [[1 2 3]
  [4 5 6]
  [7 8 9]]]

# print(q[1, 1:, :2])
[[4 5]
 [7 8]]


# print(q[1, 1, 1])
5
```

Main methods:

```python
ndarray.flatten() # превращает массив в одномерный.
ndarray.transpose(*axes) # транспонирование (или смена порядка осей в случае, когда размерность массива больше двух).
ndarray.T == q.transpose() # True
ndarray.reshape(shape) # смена формы массива. Массив "распрямляется" и построчно заполняется в новую форму.
ndarray.dot(other_ndarray) # матричное произведение
ndarray @ other_ndarray == ndarray.dot(other_ndarray) # True

ndarray.min(axis=None) # минимальное значение
ndarray.max(axis=None) # максимальное значение
ndarray.mean(axis=None) # среднее значение
ndarray.sum(axis=None) # сумма
ndarray.prod(axis=None) # произведение
ndarray.cumsum(axis=None) # кумулятивная сумма (a1, a1+a2, ⋯, a1+⋯+an)
ndarray.prod(axis=None) # кумулятивное произведение (a1, a1*a2, ⋯, a1*⋯*an)
```

---

### np.linalg

Core Linear Algebra Tools

Main methods:
```python
linalg.matrix_power(M, n) # возведение матрицы M в степень n
linalg.norm(a, ord=None) # норма матрицы a, по умолчанию норма Фробениуса для матриц и L2-норма для векторов. Перечень норм в [справке](http://docs.scipy.org/doc/numpy/reference/generated/numpy.linalg.norm.html#numpy.linalg.norm)
linalg.inv(a) # матрица, обратная к a (если a необратима, выбрасывается LinAlgError; псевдообратная считается через linalg.pinv(a))
```

---

### np.logical_*

[logical_not](http://docs.scipy.org/doc/numpy-1.10.0/reference/generated/numpy.logical_not.html) 
[logical_and](http://docs.scipy.org/doc/numpy-1.10.0/reference/generated/numpy.logical_and.html#numpy.logical_and)
[logical_or](http://docs.scipy.org/doc/numpy-1.10.0/reference/generated/numpy.logical_or.html#numpy.logical_or)
[logical_xor](http://docs.scipy.org/doc/numpy-1.10.0/reference/generated/numpy.logical_xor.html#numpy.logical_xor)

```python
import numpy as np

q = np.array([True, False, 1, 0])
w = np.logical_not(q)
e = np.logical_not(w)
print("q =", q)
print("w =", w)
print("e =", e)

# q = [1 0 1 0]
# w = [False  True False  True]
# e = [ True False  True False]
```

---

### np.vectorize

*Аналог стандартной функции ```map```*
На входе берёт функцию преобразования элемента ndarray и превращает его в такой элемент, который нужен.

Пример:

```python
def myfunc(a, b):
    "Return a-b if a>b, otherwise return a+b"
    if a > b:
        return a - b
    else:
        return a + b

vfunc = np.vectorize(myfunc)
vfunc([1, 2, 3, 4], 2)
# >>> array([3, 4, 1, 2])
```