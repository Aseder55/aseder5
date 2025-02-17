# Практика 7

## Цель работы

1. Изучить возможности технологии Apache Arrow для обработки и анализ больших
данных
2. Получить навыки применения Arrow совместно с языком программирования R
3. Получить навыки анализа метаинфомации о сетевом трафике
4. Получить навыки применения облачных технологий хранения, подготовки и
анализа данных: Yandex Object Storage, Rstudio Server.

## План

1.  Импортировать данные с помощью функции open_dataset
2.  Выполнить задания

## Шаги

1.  Импортируем данные с помощью библиотеки arrow

```{r}
library(arrow)
library(dplyr)
library(tidyverse)
#download.file("https://storage.yandexcloud.net/arrow-datasets/tm_data.pqt",destfile = "tm_data.pqt")
df <- arrow::open_dataset(sources = "tm_data.pqt", format = "parquet")
glimpse(df)
```
```{r}
glimpse(df)
```

2.  Приступаем к выполнению заданий

  a.  Найдите утечку данных из вашей сети
    
```{r}
task1 <- df %>% filter(str_detect(src, "^12.") | str_detect(src, "^13.") | str_detect(src, "^14."))  %>% filter(!str_detect(dst, "^12.") & !str_detect(dst, "^13.") & !str_detect(dst, "^14."))  %>% group_by(src) %>% summarise("sum" = sum(bytes)) %>% arrange(desc(sum)) %>% head(1) %>% select(src) 
task1 %>% collect() %>% knitr::kable()
```
    
  b.  Найдите утечку данных 2
    
  Для начала нужно определить рабочее время. Для этого можно использовать нагрузку на трафик, и выцепить час с сортировкой по количеству трафика.
    
```{r}
task21 <- df %>% select(timestamp, src, dst, bytes) %>% mutate(trafic = (str_detect(src, "^((12|13|14)\\.)") & !str_detect(dst, "^((12|13|14)\\.)")),time = hour(as_datetime(timestamp/1000))) %>% filter(trafic == TRUE, time >= 0 & time <= 24) %>% group_by(time) %>%
summarise(trafictime = n()) %>% arrange(desc(trafictime))
task21 %>% collect() %>% knitr::kable()
```
    
  По данным выясняем, что рабочим временем является 16-23. 
    
```{r}
task22 <- df %>% mutate(time = hour(as_datetime(timestamp/1000))) %>% 
filter(!str_detect(src, "^13.37.84.125")) %>%  filter(str_detect(src, "^12.") | str_detect(src, "^13.") | str_detect(src, "^14."))  %>% filter(!str_detect(dst, "^12.") | !str_detect(dst, "^13.") | !str_detect(dst, "^14."))  %>% filter(time >= 1 & time <= 15) %>%  group_by(src) %>% summarise("sum" = sum(bytes)) %>% arrange(desc(sum)) %>% head(1) %>% select(src) 
task22 %>% collect() %>% knitr::kable()
```
    
  c.  Найдите утечку данных 3
    
```{r}
task31 <- df %>% filter(!str_detect(src, "^13.37.84.125")) %>% filter(!str_detect(src, "^12.55.77.96")) %>% filter(str_detect(src, "^12.") | str_detect(src, "^13.") | str_detect(src, "^14."))  %>% filter(!str_detect(dst, "^12.") & !str_detect(dst, "^13.") & !str_detect(dst, "^14."))  %>% select(src, bytes, port) 


task31 %>%  group_by(port) %>% summarise("mean"=mean(bytes), "max"=max(bytes), "sum" = sum(bytes)) %>% 
  mutate("Raz"= max-mean)  %>% filter(Raz!=0) %>% arrange(desc(Raz)) %>% head(1) %>% collect() %>% knitr::kable()
```
    
```{r}
task32 <- task31  %>% filter(port==37) %>% group_by(src) %>% summarise("mean"=mean(bytes)) %>% arrange(desc(mean)) %>% head(1) %>% select(src)
task32 %>% collect() %>% knitr::kable()
```

## Оценка результата

Был скачан и проанализирован пакет данных tm_data, были выполнены три задания.

## Вывод

Я ознакомился с применением облачных технологий хранения, подготовки и анализа данных, а также проанализировал метаинформацию о сетевом трафике.
