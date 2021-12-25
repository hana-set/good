---
title:  "데이터 살펴보기"
excerpt: "R 데이터를 어떻게 살펴볼 지 알아봅시다."
categories:
  - R_Basic
tags:
  - 전처리
last_modified_at: 2021-01-02T06:24:00

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
---
데이터 살펴보기
================

데이터를 전처리 하기 전에 어떤 형태인지 알아봐야 할 것이다.<br> 그럴때는 아래와 같이 데이터를 살펴보기 위한 명령어들이다.

## head

데이터의 앞부분을 보여준다.<br> **n** : default 는 5이지만, 수를 지정해서 원하는만큼의 데이터를 볼 수 있다.

``` r
head(iris,n=7)
```

    ##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ## 1          5.1         3.5          1.4         0.2  setosa
    ## 2          4.9         3.0          1.4         0.2  setosa
    ## 3          4.7         3.2          1.3         0.2  setosa
    ## 4          4.6         3.1          1.5         0.2  setosa
    ## 5          5.0         3.6          1.4         0.2  setosa
    ## 6          5.4         3.9          1.7         0.4  setosa
    ## 7          4.6         3.4          1.4         0.3  setosa

## tail

데이터의 뒷부분을 보여준다.<br> **n** : default 는 5이지만, 수를 지정해서 원하는만큼의 데이터를 볼 수 있다.

``` r
tail(iris,n = 10)
```

    ##     Sepal.Length Sepal.Width Petal.Length Petal.Width   Species
    ## 141          6.7         3.1          5.6         2.4 virginica
    ## 142          6.9         3.1          5.1         2.3 virginica
    ## 143          5.8         2.7          5.1         1.9 virginica
    ## 144          6.8         3.2          5.9         2.3 virginica
    ## 145          6.7         3.3          5.7         2.5 virginica
    ## 146          6.7         3.0          5.2         2.3 virginica
    ## 147          6.3         2.5          5.0         1.9 virginica
    ## 148          6.5         3.0          5.2         2.0 virginica
    ## 149          6.2         3.4          5.4         2.3 virginica
    ## 150          5.9         3.0          5.1         1.8 virginica

## View

데이터 내용을 새 윈도우를 열어서 보여준다.<br> 오름차순으로 정렬하거나 다양한 조작 가능<br>

``` r
View(iris)
```

## dim

데이터의 차원을 보여준다.

``` r
dim(iris)
```

    ## [1] 150   5

## length

length(df) : 데이터프레임에 사용시 column 의 갯수 출력 <br> length(df$col) : column 에
사용시 col 의 element 의 갯수 출력<br>

``` r
length(iris) 
```

    ## [1] 5

``` r
length(iris$Sepal.Length) 
```

    ## [1] 150

## names

데이터의 구성요소 이름 (col 의 이름)을 출력한다.

``` r
names(iris)
```

    ## [1] "Sepal.Length" "Sepal.Width"  "Petal.Length" "Petal.Width"  "Species"

## summary

데이터의 기초 통계량을 보여준다.

``` r
summary(iris)
```

    ##   Sepal.Length    Sepal.Width     Petal.Length    Petal.Width   
    ##  Min.   :4.300   Min.   :2.000   Min.   :1.000   Min.   :0.100  
    ##  1st Qu.:5.100   1st Qu.:2.800   1st Qu.:1.600   1st Qu.:0.300  
    ##  Median :5.800   Median :3.000   Median :4.350   Median :1.300  
    ##  Mean   :5.843   Mean   :3.057   Mean   :3.758   Mean   :1.199  
    ##  3rd Qu.:6.400   3rd Qu.:3.300   3rd Qu.:5.100   3rd Qu.:1.800  
    ##  Max.   :7.900   Max.   :4.400   Max.   :6.900   Max.   :2.500  
    ##        Species  
    ##  setosa    :50  
    ##  versicolor:50  
    ##  virginica :50  
    ##                 
    ##                 
    ## 

## class

데이터의 속성을 나타낸다.

``` r
class(iris) # iris 의 속성은 data.frame
```

    ## [1] "data.frame"

``` r
class(c(1,2,3)) # 벡터는 한 속성의 element로 구성된다. 즉 vector 의 구성인 numeric 표출
```

    ## [1] "numeric"

``` r
class(c(1,2,'a')) # 벡터는 한 속성의 element 가 되야되서 character 표출
```

    ## [1] "character"

## str

데이터의 내부 구조를 보여준다.

``` r
str(iris) # 범주형의 경우 어떤 level 로 구성되어있고, 각 data type 이 뭔지
```

    ## 'data.frame':    150 obs. of  5 variables:
    ##  $ Sepal.Length: num  5.1 4.9 4.7 4.6 5 5.4 4.6 5 4.4 4.9 ...
    ##  $ Sepal.Width : num  3.5 3 3.2 3.1 3.6 3.9 3.4 3.4 2.9 3.1 ...
    ##  $ Petal.Length: num  1.4 1.4 1.3 1.5 1.4 1.7 1.4 1.5 1.4 1.5 ...
    ##  $ Petal.Width : num  0.2 0.2 0.2 0.2 0.2 0.4 0.3 0.2 0.2 0.1 ...
    ##  $ Species     : Factor w/ 3 levels "setosa","versicolor",..: 1 1 1 1 1 1 1 1 1 1 ...

## attach : 데이터를 고정해서 사용한다.

``` r
attach(iris)
Sepal.Length # 원래 iris$Sepal.Length 로 해야하지만, attcach 로 해서 바로나온다.
```

    ##   [1] 5.1 4.9 4.7 4.6 5.0 5.4 4.6 5.0 4.4 4.9 5.4 4.8 4.8 4.3 5.8 5.7 5.4 5.1
    ##  [19] 5.7 5.1 5.4 5.1 4.6 5.1 4.8 5.0 5.0 5.2 5.2 4.7 4.8 5.4 5.2 5.5 4.9 5.0
    ##  [37] 5.5 4.9 4.4 5.1 5.0 4.5 4.4 5.0 5.1 4.8 5.1 4.6 5.3 5.0 7.0 6.4 6.9 5.5
    ##  [55] 6.5 5.7 6.3 4.9 6.6 5.2 5.0 5.9 6.0 6.1 5.6 6.7 5.6 5.8 6.2 5.6 5.9 6.1
    ##  [73] 6.3 6.1 6.4 6.6 6.8 6.7 6.0 5.7 5.5 5.5 5.8 6.0 5.4 6.0 6.7 6.3 5.6 5.5
    ##  [91] 5.5 6.1 5.8 5.0 5.6 5.7 5.7 6.2 5.1 5.7 6.3 5.8 7.1 6.3 6.5 7.6 4.9 7.3
    ## [109] 6.7 7.2 6.5 6.4 6.8 5.7 5.8 6.4 6.5 7.7 7.7 6.0 6.9 5.6 7.7 6.3 6.7 7.2
    ## [127] 6.2 6.1 6.4 7.2 7.4 7.9 6.4 6.3 6.1 7.7 6.3 6.4 6.0 6.9 6.7 6.9 5.8 6.8
    ## [145] 6.7 6.7 6.3 6.5 6.2 5.9

## detach : 데이터 고정을 해재한다.

``` r
detach(iris)
# Sepal.Length # 이렇게 실행하면 오류가 난다.
iris$Sepal.Length 
```

    ##   [1] 5.1 4.9 4.7 4.6 5.0 5.4 4.6 5.0 4.4 4.9 5.4 4.8 4.8 4.3 5.8 5.7 5.4 5.1
    ##  [19] 5.7 5.1 5.4 5.1 4.6 5.1 4.8 5.0 5.0 5.2 5.2 4.7 4.8 5.4 5.2 5.5 4.9 5.0
    ##  [37] 5.5 4.9 4.4 5.1 5.0 4.5 4.4 5.0 5.1 4.8 5.1 4.6 5.3 5.0 7.0 6.4 6.9 5.5
    ##  [55] 6.5 5.7 6.3 4.9 6.6 5.2 5.0 5.9 6.0 6.1 5.6 6.7 5.6 5.8 6.2 5.6 5.9 6.1
    ##  [73] 6.3 6.1 6.4 6.6 6.8 6.7 6.0 5.7 5.5 5.5 5.8 6.0 5.4 6.0 6.7 6.3 5.6 5.5
    ##  [91] 5.5 6.1 5.8 5.0 5.6 5.7 5.7 6.2 5.1 5.7 6.3 5.8 7.1 6.3 6.5 7.6 4.9 7.3
    ## [109] 6.7 7.2 6.5 6.4 6.8 5.7 5.8 6.4 6.5 7.7 7.7 6.0 6.9 5.6 7.7 6.3 6.7 7.2
    ## [127] 6.2 6.1 6.4 7.2 7.4 7.9 6.4 6.3 6.1 7.7 6.3 6.4 6.0 6.9 6.7 6.9 5.8 6.8
    ## [145] 6.7 6.7 6.3 6.5 6.2 5.9

## with : 데이터를 활성화한다. attach 와 비슷

``` r
with(iris,max(Sepal.Length))
```

    ## [1] 7.9
