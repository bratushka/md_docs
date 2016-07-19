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

### DataFrame

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

df$Name[1:2]
# Olga   Marina
# Levels: Katya Marina Olga Viktor
df[1,1]
# Olga
# Levels: Katya Marina Olga Viktor
df[1,]
#   Name Age Married
# 1 Olga  23    TRUE
df[,1]
# Olga   Marina Katya  Viktor
# Levels: Katya Marina Olga Viktor
subset(df1, Age < 24.5)
#     Name Age Married
# 1   Olga  23    TRUE
# 2 Marina  24    TRUE

typeof(df)
# "list"
nrow(df)
# 4
ncol(df)
# 3
head.(df)
# shows first 6 rows
tail.(df)
# shows last 6 rows
View(df)
# shows data as a table
str(df)
# 'data.frame':	4 obs. of  3 variables:
# $ Name   : Factor w/ 4 levels "Katya","Marina",..: 3 2 1 4
# $ Age    : int  23 24 25 26
# $ Married: logi  TRUE TRUE FALSE FALSE
names(df)
# "Name"    "Age"     "Married"
summary(df)
#     Name        Age         Married       
# Katya :1   Min.   :23.00   Mode :logical  
# Marina:1   1st Qu.:23.75   FALSE:2        
# Olga  :1   Median :24.50   TRUE :2        
# Viktor:1   Mean   :24.50   NA's :0        
#            3rd Qu.:25.25                  
#            Max.   :26.00  

df$Age
# 23 24 25 26
df$DoubleAge <- df$Age * 2
#     Name Age Married DoubleAge
# 1   Olga  23    TRUE        46
# 2 Marina  24    TRUE        48
# 3  Katya  25   FALSE        50
# 4 Viktor  26   FALSE        52
df$NewVariable <- 0
#     Name Age Married DoubleAge NewVariable
# 1   Olga  23    TRUE        46           0
# 2 Marina  24    TRUE        48           0
# 3  Katya  25   FALSE        50           0
# 4 Viktor  26   FALSE        52           0

rbind() # join dataframes by rows (vertically)
cbind() # join dataframes by columns (horizontally)

read.table() # reads any file
read.csv() # reads comma separated file
read.csv2() # reads semicolon separated file

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