# R

[TOC]

---

### Vector

Создание вектора
```py
vec_1 <- c(1, 2, 4, 8)
# num [1:4] 1 2 4 8
vec_1[1]
# 1
vec_1[c(1, 3)]
# 1 4
vec_1[1:3]
# 1 2 4
vec_1[5]
# NA
vec_1 == 2
# FALSE  TRUE FALSE FALSE
vec_1[vec_1 > 2]
# 4 8
vec_1[vec_1 > 2 & vec_1 < 7]
# 4

vec_2 <- 1:4
# int [1:4] 1 2 3 4

vec_3 <- vec_1 + vec_2
# num [1:4] 2 4 7 12

vec_4 <- c(vec_2, vec_3)
# num [1:4] 1 2 3 4 2 4 7 12

vec_5 <- vec_1 + 1
# num [1:4] 2 3 5 9
```

---

### List

```py
vec_1 = c(1,2,4,8)
vec_2 = c(T,F,T,F)

l_1 = list(vec_1, vec_2)
# [[1]]
# 1 2 4 8
# [[2]]
# TRUE FALSE  TRUE FALSE

l_1[[1]][2]
# 2
```

---

### data.frame

```py
name = c("Olga", "Marina", "Katya", "Viktor")
age = 23:26
married = c(T,T,F,F)
df <- data.frame(Name=name, Age=age, Married=married)
#     Name Age Married
# 1   Olga  23    TRUE
# 2 Marina  24    TRUE
# 3  Katya  25   FALSE
# 4 Viktor  26   FALSE

typeof(df)
# "list"

```

---

### Basic operations

```py
vec <- 1:9

min(vec)
# 1
max(vec)
# 9
mean(vec)
# 5
sum(vec)
# 45
prod(vec)
# 362880
sd(vec)
# 2.738613
abs(-2)
# 2

5^2 # 5**2
# 25
5 %% 2
# 1
5 %/% 2
# 2
```