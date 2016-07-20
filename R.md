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
df[,-c(2,3)]
#     Name
# 1   Olga
# 2 Marina
# 3  Katya
# 4 Viktor
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
median(vec)
# 5
range(vec)
# 1 9

5^2 # 5**2
# 25
5 %% 2
# 1
5 %/% 2
# 2
vec %in% 3:5
# FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
```

---

### Conditions and cycles

```py
if (1 > 0) {
  print("true")
} else {
  print("false")
}
# "true"

ifelse(-2:2 > 0, T, F)
# FALSE FALSE FALSE  TRUE  TRUE

for (i in 1:3) {
  print(i)
}
# 1
# 2
# 3

while (var > 0) {
  print(var)
  var <- var-1
}
# 3
# 2
# 1
```

---

### Complex statistics

```py
df <- mtcars

# Get the mean `hp` for all cars, splitted by `vs` parameter
mean_hp_by_vs = aggregate(x = df$hp, by = list(df$vs), FUN = mean)
colnames(mean_hp_by_vs) <- c("VS", "Mean HP")
#   VS   Mean HP
# 1  V 189.72222
# 2  S  91.35714
aggregate(hp ~ vs, df, mean)
#   vs        hp
# 1  V 189.72222
# 2  S  91.35714
aggregate(hp ~ vs + am, df, mean) # aggregate(x = df$hp, by = list(df$vs, df$am), FUN = mean)
#   vs     am        hp
# 1  V   Auto 194.16667
# 2  S   Auto 102.14286
# 3  V Manual 180.83333
# 4  S Manual  80.57143
aggregate(x = df[, -c(8,9)], by = list(df$am), FUN = median)
#   Group.1  mpg cyl  disp  hp drat   wt  qsec gear carb
# 1    Auto 17.3   8 275.8 175 3.15 3.52 17.82    3    3
# 2  Manual 22.8   4 120.3 109 4.08 2.32 17.02    4    2
aggregate(cbind(mpg, disp) ~ am, df, median)
#       am  mpg  disp
# 1   Auto 17.3 275.8
# 2 Manual 22.8 120.3
```

---

### Libraries

```py
install.packages("ggplot2") # install `ggplot2` package
library(ggplot2) # load all methods from `ggplot2`
```

---

### Psych

```py
df <- mtcars
psych::describe(df)
#      vars  n   mean     sd median trimmed    mad   min    max  range  skew kurtosis    se
# mpg     1 32  20.09   6.03  19.20   19.70   5.41 10.40  33.90  23.50  0.61    -0.37  1.07
# cyl     2 32   6.19   1.79   6.00    6.23   2.97  4.00   8.00   4.00 -0.17    -1.76  0.32
# disp    3 32 230.72 123.94 196.30  222.52 140.48 71.10 472.00 400.90  0.38    -1.21 21.91
# hp      4 32 146.69  68.56 123.00  141.19  77.10 52.00 335.00 283.00  0.73    -0.14 12.12
# drat    5 32   3.60   0.53   3.70    3.58   0.70  2.76   4.93   2.17  0.27    -0.71  0.09
# wt      6 32   3.22   0.98   3.33    3.15   0.77  1.51   5.42   3.91  0.42    -0.02  0.17
# qsec    7 32  17.85   1.79  17.71   17.83   1.42 14.50  22.90   8.40  0.37     0.34  0.32
# vs      8 32   0.44   0.50   0.00    0.42   0.00  0.00   1.00   1.00  0.24    -2.00  0.09
# am      9 32   0.41   0.50   0.00    0.38   0.00  0.00   1.00   1.00  0.36    -1.92  0.09
# gear   10 32   3.69   0.74   4.00    3.62   1.48  3.00   5.00   2.00  0.53    -1.07  0.13
# carb   11 32   2.81   1.62   2.00    2.65   1.48  1.00   8.00   7.00  1.05     1.26  0.29

descr_by = psych::describeBy(mtcars, group = list(df$vs))
# : 0
#      vars  n   mean     sd median trimmed   mad    min    max  range  skew kurtosis    se
# mpg     1 18  16.62   3.86  15.65   16.42  2.97  10.40  26.00  15.60  0.48    -0.05  0.91
# cyl     2 18   7.44   1.15   8.00    7.62  0.00   4.00   8.00   4.00 -1.74     1.94  0.27
# disp    3 18 307.15 106.77 311.00  308.52 72.65 120.30 472.00 351.70 -0.26    -1.06 25.16
# hp      4 18 189.72  60.28 180.00  186.81 48.18  91.00 335.00 244.00  0.45    -0.15 14.21
# drat    5 18   3.39   0.47   3.18    3.37  0.32   2.76   4.43   1.67  0.74    -0.73  0.11
# wt      6 18   3.69   0.90   3.57    3.68  0.50   2.14   5.42   3.28  0.54    -0.43  0.21
# qsec    7 18  16.69   1.09  17.02   16.75  0.85  14.50  18.00   3.50 -0.71    -0.80  0.26
# vs      8 18   0.00   0.00   0.00    0.00  0.00   0.00   0.00   0.00   NaN      NaN  0.00
# am      9 18   0.33   0.49   0.00    0.31  0.00   0.00   1.00   1.00  0.65    -1.66  0.11
# gear   10 18   3.56   0.86   3.00    3.50  0.00   3.00   5.00   2.00  0.90    -1.07  0.20
# carb   11 18   3.61   1.54   4.00    3.44  1.48   2.00   8.00   6.00  1.17     1.33  0.36
# ------------------------------------------------------------------- 
# : 1
#      vars  n   mean    sd median trimmed   mad   min    max  range  skew kurtosis    se
# mpg     1 14  24.56  5.38  22.80   24.34  6.00 17.80  33.90  16.10  0.41    -1.40  1.44
# cyl     2 14   4.57  0.94   4.00    4.50  0.00  4.00   6.00   2.00  0.85    -1.36  0.25
# disp    3 14 132.46 56.89 120.55  127.11 61.82 71.10 258.00 186.90  0.80    -0.49 15.21
# hp      4 14  91.36 24.42  96.00   92.00 32.62 52.00 123.00  71.00 -0.24    -1.61  6.53
# drat    5 14   3.86  0.51   3.92    3.86  0.26  2.76   4.93   2.17 -0.28     0.46  0.14
# wt      6 14   2.61  0.72   2.62    2.63  0.95  1.51   3.46   1.95 -0.17    -1.68  0.19
# qsec    7 14  19.33  1.35  19.17   19.24  1.02 16.90  22.90   6.00  0.86     1.25  0.36
# vs      8 14   1.00  0.00   1.00    1.00  0.00  1.00   1.00   0.00   NaN      NaN  0.00
# am      9 14   0.50  0.52   0.50    0.50  0.74  0.00   1.00   1.00  0.00    -2.14  0.14
# gear   10 14   3.86  0.53   4.00    3.83  0.00  3.00   5.00   2.00 -0.17    -0.09  0.14
# carb   11 14   1.79  1.05   1.50    1.67  0.74  1.00   4.00   3.00  1.13    -0.03  0.28
#
# `descr_by` is a list. We can access the 2 matrix by descr_by$`0` and descr_by$`1`
# In order to get a matrix in `descr_by` we should do `psych::describeBy(..., mat = TRUE)`

```