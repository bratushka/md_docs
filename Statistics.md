# Статистика

[TOC]

---

### Среднеквадратическое отклонение

**Среднеквадрати́ческое отклоне́ние** (*синонимы: среднее квадрати́ческое отклоне́ние, среднеквадрати́чное отклоне́ние, квадрати́чное отклоне́ние; близкие термины: станда́ртное отклоне́ние, станда́ртный разбро́с*) —
в теории вероятностей и статистике наиболее распространённый показатель рассеивания значений случайной величины относительно её математического ожидания. При ограниченных массивах выборок значений вместо математического ожидания используется среднее арифметическое совокупности выборок.

Среднеквадратическое отклонение измеряется в единицах измерения самой случайной величины и используется при расчёте стандартной ошибки среднего арифметического, при построении доверительных интервалов, при статистической проверке гипотез, при измерении линейной взаимосвязи между случайными величинами. Определяется как квадратный корень из дисперсии случайной величины.

***Формула*** дисперсии
$$
\sigma^2 = \frac{1}{n} \sum^n_{i=1} (x_i - \bar x)^2
$$

***Формула*** cреднеквадратического отклонения
$$
\sigma = \sqrt {\frac{1}{n} \sum^n_{i=1} (x_i - \bar x)^2}
$$

***Формула*** стандартного отклонения (оценка среднеквадратического отклонения случайной величины x относительно её математического ожидания на основе несмещённой оценки её дисперсии)
$$
s = \sqrt {\frac{n}{n-1}\sigma^2} = \sqrt {\frac{1}{n-1}\sum^n_{i=1} (x_i - \bar x)^2}
$$

---

### Правило трёх сигм

Правило трёх сигм ($3\sigma$) — практически все значения нормально распределённой случайной величины лежат в интервале $(\bar x - 3\sigma; \bar x + 3\sigma)$ . Более строго — приблизительно с вероятностью 0,9973 значение нормально распределённой случайной величины лежит в указанном интервале (при условии, что величина $\bar x$  истинная, а не полученная в результате обработки выборки).

Если же истинная величина $\bar x$  неизвестна, то следует пользоваться не $\sigma$, а $s$. Таким образом, правило трёх сигм преобразуется в правило трёх s.

---

### Однофакторный дисперсионный анализ

Допустим имеется 3 группы наблюдений

$$
\begin{matrix}
_1 & _2 & _3\\
3 & 5 & 7\\
1 & 3 & 6\\
2 & 4 & 5
\end{matrix}
$$

Нулевая гипотеза $H_0$ состоит в том, что в генеральной совокупности нет значимых различий между средними выборок, то-есть $M_1 = M_2 = M_3$
Под $H_0$ принимается та гипотеза, которая нам выгодна, таким образом ошибка первого рода (которая считается более опастной) играет нам на руку.
Альтернативная гипотез $H_1$ говорит о том, что хотя бы одно среднее среди выборок значимо отличается от остальных.

$$
\bar{\bar x} = \frac{\sum^n_{i=0}x_i}{n} = \frac{36}{9} = 4
$$

***SST*** (или ***TSS***) - Total Sum of Squares - общая сумма квадратов. Характеризует изменчивость данных без учёта разделения их на группы.

***dF*** - количество степеней свободы. Фактически - число независимых элементов при рассчёте некоторого показателя.

$$
SST = (3-4)^2 + (1-4)^2 \dots (6-4)^2 + (5-4)^2 = 30
$$
$$
dF = N - 1 = 8
$$

***SSB*** - Sum of Squares Between (Groups) - межгрупповая сумма квадратов

***SSW*** - Sum of Squares Within (Groups) - внутригрупповая сумма квадратов

$\bar x_1=2$
$\bar x_2=4$
$\bar x_3=6$

$$
SSW = (3-2)^2 + \dots + (5-4)^2 + \dots + (7-6)^2 = 6
$$
Количество степеней свобод для SSW - количество элементов минус количество групп. $dF = N-m = 9-3 = 6$

$$
SSB = \sum_{i=1}^n m(\bar x_i - \bar{\bar x}) = 3(2-4)^2 + 3(4-4)^2 + 3(6-4)^2 = 24
$$

Количество степеней свобод для SSB - количество групп минус 1. $dF = m-1 = 3-1 = 2$

Выводы:
1. если  $SSB > SSW$ - это значит, что группы значительно различаются между собой
1. если  $SSB < SSW$ - это значит, что группы не различаются между собой и изменчивость существует только внутри групп

Основной статистический показатель дисперсионного анализа ***F***
$$
F = \frac{\frac{SSB}{dF_{SSB}}}{\frac{SSW}{dF_{SSW}}} = \frac{\frac{SSB}{m-1}}{\frac{SSW}{N-m}} = \frac{\frac{24}{2}}{\frac{6}{6}} = 12
$$

Чем меньше $F$ , тем более вероятно, что группы принадлежат к одной и той же выборке.

---

### Ошибки

1. *Ошибка первого рода* - найти различия там, где их нет
1. *Ошибка второго рода* - не найти различия там, где они есть

---

### Поправка Бонферрони

При сравнении нескольких групп во время однофакторного анализа необходимо делать корректировку $P$ уровня значимости.
$$
P_1 = \frac{P_0}{количество\ попарных\ сравнений}
$$
Например:
1. P_0 = 0.05 (стандартный P уровень значимости)
1. m = 8 (количество сравниваемых групп)

Тогда количество попарных сравнений будет равно $m(m-1)/2 = 8(8-1)/2 = 28$
Соответственно $P_1 = 0.05 / 28 = 0.001785714$

---

### Поправка Тьюки (Tukey HSD)

Более либеральный метод получения поправки. Гугли.

---

### Двухфакторный дисперсионны анализ

*A* - первый фактор
*B* - второй фактор
$$
SST = SSW + SSB_A + SSB_B + SSB_A*SSB_B
$$

---

### Корелляция

***Ковариация*** - сумма произведений отклонений от средних значений делённая на число степеней свобод:
$$
cov = \frac{\sum^n_{i=1} (x_i - \bar x) (y_i - \bar y)}{N-1}
$$

***Корелляция*** - показатель силы и направления взаимосвязи двух количественных переменных.
Коэффициент корелляции (Пирсона) равняется ковариации делённой на произведение стандартных отклонений факторов (находится в пределах [-1; 1])
$$
r_{xy} = \frac{cov}{\delta_x \delta_y}
$$

***Коэффициент детерминации*** - ($R^2$) - коэффициент, показывающий в какой степени дисперсия одной переменной обусловлена "влиянием" другой переменной (принимает значения [0; 1]).
$$
R^2 = r_{xy}^2
$$

---

### Регрессионный анализ

Требования:

1. Линейная зависимость $y$ от $x$
1. Нормальное распределение остатков
1. Гомоскедастичность - постоянная изменчивость остатков на всех уровнях независимой переменной

Формула регрессии:
$$
\hat y = b_0 + b_1 x
$$

$$
b_1 = \frac{стандартное\ отклонение\ по\ y}{стандартное\ отклонение\ по\ x}r_{xy} = \frac{sd_y}{sd_x}r_{xy}
$$

$$
b_0 = \bar y - b_1 \bar x
$$

---

### Множественная регрессия

Требования:

1. Требования обычного регрессионного анализа
1. Проверка на мультиколлинеарность (очень сильная взаимосвязь между некоторыми переменными)
1. Нормальное распределение переменных