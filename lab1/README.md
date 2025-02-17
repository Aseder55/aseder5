# Лабораторная пработа 1

## Цель работы

1.  Развить практические навыки использования языка программирования R для обработки данных
2.  Развить навыки работы в Rstudio IDE: установка пакетов работа с проектами в Rstudio настройка и работа с Git
3.  Закрепить знания базовых типов данных языка R и простейших операций с ними

## Исходные данные

1.  Программное обеспечение Windows 10 Pro
2.  Rstudio Desktop
3.  Интерпретатор языка R 4.1.1

## План

Используя программный пакет swirl, освоить базовые операции в языке программирования R.

## Шаги:

### 1. Установить программный пакет swirl

```{r}
install.packages("swirl")
```
### 2. Запустить задание с помощью swirl::swirl()

```{r}
swirl::swirl()
```

### 3. Выполнение basic Building Blocks

```{r}
5+7
```
```{r}
x<-5+7
```
```{r}
x
```
```{r}
y<-x-3
```
```{r}
y
```
```{r}
z<-c(1.1, 9, 3.14)
```
```{r}
?c
```
```{r}
z
```
```{r}
z*2+100
```
```{r}
my_sqrt <- sqrt(z - 1)
```
```{r}
my_sqrt
```
```{r}
my_div <- z/my_sqrt
```
```{r}
my_div
```
```{r}
c(1, 2, 3, 4) + c(0, 10)
```
```{r}
c(1, 2, 3, 4) + c(0, 10, 100)
```
```{r}
z * 2 + 1000
```
```{r}
my_div
```
### 4.Выполнение Workspace and Files

```{r}
getwd()
```
```{r}
ls()
```
```{r}
x <- 9
```
```{r}
ls()
```
```{r}
dir()
```
```{r}
?list.files
```
```{r}
args(list.files)
```
```{r}
old.dir <- getwd()
```
```{r}
dir.create("testdir")
```
```{r}
setwd("testdir")
```
```{r}
file.create("mytest.R")
```
```{r}
list.files()
```
```{r}
file.exists("mytest.R")
```
```{r}
file.info("mytest.R")
```
```{r}
file.rename("mytest.R", "mytest2.R")
```
```{r}
file.copy("mytest2.R", "mytest3.R")
```
```{r}
file.path("mytest3.R")
```
```{r}
file.path("folder1", "folder2")
```
```{r}
?dir.create
```
```{r}
dir.create(file.path('testdir2', 'testdir3'), recursive = TRUE)
```
```{r}
setwd(old.dir)
```
### 5. Выполнение Sequences of Numbers
```{r}
1:20
```

```{r}
pi:10
```
```{r}
15:1
```
```{r}
?`:`
```
```{r}
seq(1, 20)
```
```{r}
seq(0, 10, by=0.5) 
```
```{r}
my_seq <- seq(5, 10, length=30)
```


```{r}
length(my_seq)
```
```{r}
1:length(my_seq)
```
```{r}
seq(along.with = my_seq)
```
```{r}
seq_along(my_seq)
```
```{r}
rep(0, times = 40)
```
```{r}
rep(c(0, 1, 2), times = 10)
```

### 6. Выполнение Vectors

```{r}
rep(c(0, 1, 2), each = 10)
```
```{r}
num_vect <- c(0.5, 55, -10, 6)
```
```{r}
num_vect < 1
```
```{r}
tf <- num_vect < 1
```
```{r}
tf
```
```{r}
num_vect >= 6
```
```{r}
my_char <- c("My", "name", "is")
```
```{r}
my_char
```
```{r}
paste(my_char, collapse = " ")
```
```{r}
my_name <- c(my_char, "your_name_here")
```
```{r}
my_name
```
```{r}
paste(my_name, collapse = " ")
```
```{r}
paste("Hello", "world!", sep = " ")
```
```{r}
paste(1:3, c("X", "Y", "Z"), sep = "")
```
### 7. Выполнение Missing Values

```{r}
x <- c(44, NA, 5, NA)
```
```{r}
x*3
```
```{r}
y <- rnorm(1000)
```
```{r}
z <- rep(NA, 1000)
```
```{r}
my_data <- sample(c(y, z), 100)
```
```{r}
my_na <- is.na(my_data)
```
```{r}
my_na
```
```{r}
my_data == NA
```
```{r}
sum(my_na)
```
```{r}
my_data
```
```{r}
0/0
```
```{r}
Inf - Inf
```
## Вывод

В ходе выполненной работы я развил практические навыки использования языка программирования R для обработки данных, развил навыки работы в Rstudio IDE, используя программный пакет swirl и освоил базовые операции в языке программирования R.
