# Основы обработки данных с помощью R и Dplyr №1 Бондаренко С.А.


## Цель работы:

-   Развить практические навыки использования языка программирования R
    для обработки данных.

-   Закрепить знания базовых типов данных языка R.

-   Развить практические навыки использования функций обработки данных
    пакета dplyr функции select(), filter(), mutate(), arrange(),
    group_by().

## Исходные данные

1.  Ноутбук

2.  OC Windows

3.  Rstudio

4.  Пакет dplyr

5.  Встроенный набор данных starwars

6.  Github

## Общий план выполнения работы

1.  Установить и загрузить библиотеку dplyr.

2.  Проанализировать набор данных starwars и получить ответы на вопросы:

    -   Сколько строк в датафрейме?

    -   Сколько столбцов в датафрейме?

    -   Как просмотреть примерный вид датафрейма?

    -   Сколько уникальных рас персонажей (species) представлено в
        данных?

    -   Найти самого высокого персонажа.

    -   Найти всех персонажей ниже 170

    -   Подсчитать ИМТ (индекс массы тела) для всех персонажей.

    -   Найти 10 самых “вытянутых” персонажей. “Вытянутость” оценить по
        отношению массы (mass) к росту (height) персонажей.

    -   Найти средний возраст персонажей каждой расы вселенной Звездных
        войн.

    -   Найти самый распространенный цвет глаз персонажей вселенной
        Звездных войн.

    -   Подсчитать среднюю длину имени в каждой расе вселенной Звездных
        войн.

3.  Оформить отчет в соответствии с шаблоном

## Содержание ЛР

Для того чтобы начать выполнение задание необходимо загрузить пакет
Dplyr:

``` r
library("dplyr")
```


    Присоединяю пакет: 'dplyr'

    Следующие объекты скрыты от 'package:stats':

        filter, lag

    Следующие объекты скрыты от 'package:base':

        intersect, setdiff, setequal, union

### Шаг №1:

Сколько строк в датафрейме?

``` r
starwars %>% nrow()
```

    [1] 87

### Шаг №2:

Сколько столбцов в датафрейме?

``` r
starwars %>% ncol()
```

    [1] 14

### Шаг №3:

Как просмотреть примерный вид датафрейма?

``` r
starwars %>% glimpse()
```

    Rows: 87
    Columns: 14
    $ name       <chr> "Luke Skywalker", "C-3PO", "R2-D2", "Darth Vader", "Leia Or…
    $ height     <int> 172, 167, 96, 202, 150, 178, 165, 97, 183, 182, 188, 180, 2…
    $ mass       <dbl> 77.0, 75.0, 32.0, 136.0, 49.0, 120.0, 75.0, 32.0, 84.0, 77.…
    $ hair_color <chr> "blond", NA, NA, "none", "brown", "brown, grey", "brown", N…
    $ skin_color <chr> "fair", "gold", "white, blue", "white", "light", "light", "…
    $ eye_color  <chr> "blue", "yellow", "red", "yellow", "brown", "blue", "blue",…
    $ birth_year <dbl> 19.0, 112.0, 33.0, 41.9, 19.0, 52.0, 47.0, NA, 24.0, 57.0, …
    $ sex        <chr> "male", "none", "none", "male", "female", "male", "female",…
    $ gender     <chr> "masculine", "masculine", "masculine", "masculine", "femini…
    $ homeworld  <chr> "Tatooine", "Tatooine", "Naboo", "Tatooine", "Alderaan", "T…
    $ species    <chr> "Human", "Droid", "Droid", "Human", "Human", "Human", "Huma…
    $ films      <list> <"A New Hope", "The Empire Strikes Back", "Return of the J…
    $ vehicles   <list> <"Snowspeeder", "Imperial Speeder Bike">, <>, <>, <>, "Imp…
    $ starships  <list> <"X-wing", "Imperial shuttle">, <>, <>, "TIE Advanced x1",…

### Шаг №4:

Сколько уникальных рас персонажей (species) представлено в данных?

``` r
starwars %>% select(species) %>% filter(!is.na(species)) %>% n_distinct()
```

    [1] 37

### Шаг №5:

Найти самого высокого персонажа.

``` r
starwars %>% arrange(desc(height)) %>% head(1) %>% select(name)
```

    # A tibble: 1 × 1
      name       
      <chr>      
    1 Yarael Poof

### Шаг №6:

Найти всех персонажей ниже 170.

``` r
starwars %>% filter(height < 170) %>% select(name)
```

    # A tibble: 22 × 1
       name                 
       <chr>                
     1 C-3PO                
     2 R2-D2                
     3 Leia Organa          
     4 Beru Whitesun Lars   
     5 R5-D4                
     6 Yoda                 
     7 Mon Mothma           
     8 Wicket Systri Warrick
     9 Nien Nunb            
    10 Watto                
    # ℹ 12 more rows

### Шаг №7:

Подсчитать ИМТ (индекс массы тела) для всех персонажей. ИМТ подсчитать
по формуле 𝐼 = 𝑚 / ℎ ^ 2, где 𝑚 – масса (weight), а ℎ – рост (height).

``` r
starwars %>% mutate("I" = mass / height ^ 2) %>%  select(name, I)
```

    # A tibble: 87 × 2
       name                     I
       <chr>                <dbl>
     1 Luke Skywalker     0.00260
     2 C-3PO              0.00269
     3 R2-D2              0.00347
     4 Darth Vader        0.00333
     5 Leia Organa        0.00218
     6 Owen Lars          0.00379
     7 Beru Whitesun Lars 0.00275
     8 R5-D4              0.00340
     9 Biggs Darklighter  0.00251
    10 Obi-Wan Kenobi     0.00232
    # ℹ 77 more rows

### Шаг №8:

Найти 10 самых “вытянутых” персонажей. “Вытянутость” оценить по
отношению массы (mass) к росту (height) персонажей.

``` r
starwars %>%
  mutate(elongation = mass / height) %>%
  arrange(desc(elongation)) %>%
  select(name) %>%
  head(10) %>%
  knitr::kable()
```

<table>
<thead>
<tr class="header">
<th style="text-align: left;">name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">Jabba Desilijic Tiure</td>
</tr>
<tr class="even">
<td style="text-align: left;">Grievous</td>
</tr>
<tr class="odd">
<td style="text-align: left;">IG-88</td>
</tr>
<tr class="even">
<td style="text-align: left;">Owen Lars</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Darth Vader</td>
</tr>
<tr class="even">
<td style="text-align: left;">Jek Tono Porkins</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Bossk</td>
</tr>
<tr class="even">
<td style="text-align: left;">Tarfful</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Dexter Jettster</td>
</tr>
<tr class="even">
<td style="text-align: left;">Chewbacca</td>
</tr>
</tbody>
</table>

### Шаг №9:

Найти средний возраст персонажей каждой расы вселенной Звездных войн.

``` r
starwars %>%
  group_by(species) %>%
  summarize(avg = mean(birth_year)) %>%
  filter(!is.na(avg)) %>%
  filter(!is.na(species))
```

    # A tibble: 9 × 2
      species          avg
      <chr>          <dbl>
    1 Cerean            92
    2 Ewok               8
    3 Hutt             600
    4 Kel Dor           22
    5 Mirialan          49
    6 Mon Calamari      41
    7 Rodian            44
    8 Trandoshan        53
    9 Yoda's species   896

### Шаг №10:

Найти самый распространенный цвет глаз персонажей вселенной Звездных
войн.

``` r
starwars %>%
  group_by(species) %>%
  filter(!is.na(birth_year)) %>%
  summarise(Sr = mean(birth_year)) %>%
  select(species, Sr) 
```

    # A tibble: 15 × 2
       species           Sr
       <chr>          <dbl>
     1 Cerean          92  
     2 Droid           53.3
     3 Ewok             8  
     4 Gungan          52  
     5 Human           53.7
     6 Hutt           600  
     7 Kel Dor         22  
     8 Mirialan        49  
     9 Mon Calamari    41  
    10 Rodian          44  
    11 Trandoshan      53  
    12 Twi'lek         48  
    13 Wookiee        200  
    14 Yoda's species 896  
    15 Zabrak          54  

### Шаг №11

Подсчитать среднюю длину имени в каждой расе вселенной Звездных войн.

``` r
starwars %>%
  mutate('lenName' = nchar(name)) %>% 
  group_by(species) %>% 
  summarise('meanNameLen' = mean(lenName))
```

    # A tibble: 38 × 2
       species   meanNameLen
       <chr>           <dbl>
     1 Aleena          12   
     2 Besalisk        15   
     3 Cerean          12   
     4 Chagrian        10   
     5 Clawdite        10   
     6 Droid            4.83
     7 Dug              7   
     8 Ewok            21   
     9 Geonosian       17   
    10 Gungan          11.7 
    # ℹ 28 more rows

## Оценка результата

Были использованы знания
функций `select(), filter(), mutate(), arrange(), group_by()` для
решения практических задач.

## Вывод

В результате выполнения работы были:

-   развиты практические навыки использования языка программирования R
    для обработки данных

-   закреплены знания базовых типов данных языка R

-   развиты практические навыки использования функций обработки данных
    пакета `dplyr` – функции
    `select(), filter(), mutate(), arrange(), group_by()`
