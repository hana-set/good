---
title:  "데이터 구조 및 변환"
excerpt: "R 데이터 구조의 기초적인 내용을 알아봅시다."
categories:
  - R_Basic
tags:
  - 기초
last_modified_at: 2021-01-02T06:20:00

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
sidebar:
  nav: "docs"

---
데이터 구조및 변환
================

# 데이터 구조

R 에는 많은 데이터 구조가 있다. <br> 각각에 맞는 데이터 유형을 알아두어야 나중에 사용할 수 있을것이다.

## Scala

구성인자가 하나인 벡터

``` r
c(1)
```

    ## [1] 1

## Vector

vector 는 구성인자가 1개 이상인 1차원 구조이다. <br> vector 안의 구성인자들은 동질적이다. 즉 벡터의 모든
원소들은 같은 자료형을 가져야 한다.

``` r
c(1,2,3) # 이렇게 수행되면 동일한 숫자의 자료형을 가지게 된다.
```

    ## [1] 1 2 3

``` r
c(1,'tom',3) # 이렇게 수행되면 string(문자) 의 동일한 자료형을 가지게 된다.
```

    ## [1] "1"   "tom" "3"

``` r
x <- c('a','b','c')
names(x) <- c('first','second','third') # 이와 같이 벡터에 이름을 부여할 수 있다.
x['first'] # 그에 따라 이름을 가진 vector 가 만들어진다.
```

    ## first 
    ##   "a"

## list

생각보다 자주 사용되지는 않는다. <br> list 자료형을 사용할경우 서로 다른 타입들의 변수를 가져다가 붙일 수 있다.
<br> 그리고 서로 다른 길이, 서로 다른 차원으로 구성될 수 있다. <br>

``` r
school <- list(name = c('han','kim','hyo'),
              address = c('seoul','USA'),
              age = c(24))
# list 를 입력할때에는 위 처럼 = 를 사용해야 한다.
school # 위와 같이 class 라는 list 안에 또 다른 list 형성 가능.
```

    ## $name
    ## [1] "han" "kim" "hyo"
    ## 
    ## $address
    ## [1] "seoul" "USA"  
    ## 
    ## $age
    ## [1] 24

## list 의 접근

**$로 접근하는 list**

``` r
school$name # schoole 에서 name 의 '구성성분 추출'
```

    ## [1] "han" "kim" "hyo"

**\[\[\]\] 로 접근하는 list 구성성분 추출**

``` r
school[['name']]  # 'name' 의 구성성분 추출
```

    ## [1] "han" "kim" "hyo"

``` r
school[[1]] # name(첫번쨰) 의 구성성분 추출
```

    ## [1] "han" "kim" "hyo"

**\[\] 로 접근하는 ’ sub list’ 추출**

``` r
school['name']
```

    ## $name
    ## [1] "han" "kim" "hyo"

``` r
school[1]
```

    ## $name
    ## [1] "han" "kim" "hyo"

**\[\[\]\] 와 \[\] 의 차이** <br> \[\[\]\] : sublist 의 구성성분을 추출한다.<br> \[\]
: sublist 를 추출한다. 즉 list를 얻음<br>

``` r
class(school[1]) # sublist 추출 
```

    ## [1] "list"

``` r
class(school[[1]]) # list 에서 1번째 sublist 의 구성성분 추출
```

    ## [1] "character"

## array

동일한 유형의 데이터가 2차원 이상으로 구성

``` r
array1 = array(1:24,c(2,3,4)) # 2*3*4 array
array1
```

    ## , , 1
    ## 
    ##      [,1] [,2] [,3]
    ## [1,]    1    3    5
    ## [2,]    2    4    6
    ## 
    ## , , 2
    ## 
    ##      [,1] [,2] [,3]
    ## [1,]    7    9   11
    ## [2,]    8   10   12
    ## 
    ## , , 3
    ## 
    ##      [,1] [,2] [,3]
    ## [1,]   13   15   17
    ## [2,]   14   16   18
    ## 
    ## , , 4
    ## 
    ##      [,1] [,2] [,3]
    ## [1,]   19   21   23
    ## [2,]   20   22   24

``` r
array1[1,2,3]  # 1row,2col,3번쨰 행렬 추출
```

    ## [1] 15

## Matrix(행렬)

동일한 유형의 2차원 데이터 <br> 행렬은 모든 element 의 값들이 ‘같은’ 형태여야 합니다. <br> 즉
1,2,3,‘no’ 의 4개 element 로 구성되어있는 vector 를 matrix 로 변환시
‘1’,‘2’,‘3’,‘no’ 로 강제형변환이 됩니다. <br>

``` r
matrix(1:12,nrow=3)
```

    ##      [,1] [,2] [,3] [,4]
    ## [1,]    1    4    7   10
    ## [2,]    2    5    8   11
    ## [3,]    3    6    9   12

``` r
# nrow : row 의 수
# ncol : col 의 수
```

``` r
matrix(1:12,nrow=3,
       dimnames = list(c('a','b','c'),c('1','2','3','4')))
```

    ##   1 2 3  4
    ## a 1 4 7 10
    ## b 2 5 8 11
    ## c 3 6 9 12

``` r
# dimnames : 행과 열에 이름을 부여 (이때 다른 길이를 쓸 수 있는 list 를 써야한다.)
```

``` r
matrix(1:12,nrow=3,byrow=TRUE)
```

    ##      [,1] [,2] [,3] [,4]
    ## [1,]    1    2    3    4
    ## [2,]    5    6    7    8
    ## [3,]    9   10   11   12

``` r
# byrow : 가로로 먼저 채워지게 한다. default 는 세로(col)
```

``` r
mat <- matrix(1:12,nrow=3,
              byrow = TRUE,
              dimnames = list(c('a','b','c'),c('1','2','3','4'))) ; mat
```

    ##   1  2  3  4
    ## a 1  2  3  4
    ## b 5  6  7  8
    ## c 9 10 11 12

``` r
mat[6] # 그냥 6번째로 index 를 주게되면 col 부터 세게 되므로 10을 추출
```

    ## [1] 10

``` r
mat[2,3] # 2row, 3col 의 값
```

    ## [1] 7

``` r
mat['a','2'] # 이름으로도 추출 가능
```

    ## [1] 2

``` r
mat[1:3,1] # 범위를 추출 가능
```

    ## a b c 
    ## 1 5 9

``` r
mat[c(1,3),c(2,4)] # vector 를 이용해 추출 가능
```

    ##    2  4
    ## a  2  4
    ## c 10 12

``` r
mat['a',c(3,1)] # 이름과 같이 추출 가능
```

    ## 3 1 
    ## 3 1

## factor

factor(요인) : 범주형(명목/순서)의 데이터구조<br> 요인이 가질 수 있는값들을 수준(level) 이라고 한다.<br>
factor 는 레벨을 알파벳 순으로 정렬한다. <br> 그 다음 알파벳 순의 레벨의 정수 인덱스로 벡터 내용을 다시
만든다.<br> 펙터의 실제 내용은 레벨의 정수 인덱스이고, 각 정수를 레벨명으로 해독 가능한 범례가 있다고 생각하면
쉽다.<br>

``` r
data = c('c','a','b')
example = factor(data)
as.numeric(example) # 위를 보면 3,1,2 로 되어있음을 볼 수 있다.
```

    ## [1] 3 1 2

``` r
# 즉 알파벳 순으로 factor 를 지정해준것 
```

``` r
factor(data,levels=c('c','b','a'),ordered = T) 
```

    ## [1] c a b
    ## Levels: c < b < a

``` r
# 이렇게 하면 c,b,a 순으로 1,2,3 의 값을 매기고 ordered 가 c<b<a 로 된다.
# 즉 ordered data 를 만들고 싶을때 쓰게 된다.
```

\#\#Dataframe 데이터 유형에 상관없는 2차원데이터

``` r
name <- c('john','kim','marry')
age <- c(45,44,22)
child <- c(T,T,F)
df <- data.frame(name,age,child) ; df
```

    ##    name age child
    ## 1  john  45  TRUE
    ## 2   kim  44  TRUE
    ## 3 marry  22 FALSE

# 데이터 구조 변환

``` r
library(MASS)
str(Cars93)
```

    ## 'data.frame':    93 obs. of  27 variables:
    ##  $ Manufacturer      : Factor w/ 32 levels "Acura","Audi",..: 1 1 2 2 3 4 4 4 4 5 ...
    ##  $ Model             : Factor w/ 93 levels "100","190E","240",..: 49 56 9 1 6 24 54 74 73 35 ...
    ##  $ Type              : Factor w/ 6 levels "Compact","Large",..: 4 3 1 3 3 3 2 2 3 2 ...
    ##  $ Min.Price         : num  12.9 29.2 25.9 30.8 23.7 14.2 19.9 22.6 26.3 33 ...
    ##  $ Price             : num  15.9 33.9 29.1 37.7 30 15.7 20.8 23.7 26.3 34.7 ...
    ##  $ Max.Price         : num  18.8 38.7 32.3 44.6 36.2 17.3 21.7 24.9 26.3 36.3 ...
    ##  $ MPG.city          : int  25 18 20 19 22 22 19 16 19 16 ...
    ##  $ MPG.highway       : int  31 25 26 26 30 31 28 25 27 25 ...
    ##  $ AirBags           : Factor w/ 3 levels "Driver & Passenger",..: 3 1 2 1 2 2 2 2 2 2 ...
    ##  $ DriveTrain        : Factor w/ 3 levels "4WD","Front",..: 2 2 2 2 3 2 2 3 2 2 ...
    ##  $ Cylinders         : Factor w/ 6 levels "3","4","5","6",..: 2 4 4 4 2 2 4 4 4 5 ...
    ##  $ EngineSize        : num  1.8 3.2 2.8 2.8 3.5 2.2 3.8 5.7 3.8 4.9 ...
    ##  $ Horsepower        : int  140 200 172 172 208 110 170 180 170 200 ...
    ##  $ RPM               : int  6300 5500 5500 5500 5700 5200 4800 4000 4800 4100 ...
    ##  $ Rev.per.mile      : int  2890 2335 2280 2535 2545 2565 1570 1320 1690 1510 ...
    ##  $ Man.trans.avail   : Factor w/ 2 levels "No","Yes": 2 2 2 2 2 1 1 1 1 1 ...
    ##  $ Fuel.tank.capacity: num  13.2 18 16.9 21.1 21.1 16.4 18 23 18.8 18 ...
    ##  $ Passengers        : int  5 5 5 6 4 6 6 6 5 6 ...
    ##  $ Length            : int  177 195 180 193 186 189 200 216 198 206 ...
    ##  $ Wheelbase         : int  102 115 102 106 109 105 111 116 108 114 ...
    ##  $ Width             : int  68 71 67 70 69 69 74 78 73 73 ...
    ##  $ Turn.circle       : int  37 38 37 37 39 41 42 45 41 43 ...
    ##  $ Rear.seat.room    : num  26.5 30 28 31 27 28 30.5 30.5 26.5 35 ...
    ##  $ Luggage.room      : int  11 15 14 17 13 16 17 21 14 18 ...
    ##  $ Weight            : int  2705 3560 3375 3405 3640 2880 3470 4105 3495 3620 ...
    ##  $ Origin            : Factor w/ 2 levels "USA","non-USA": 2 2 2 2 2 1 1 1 1 1 ...
    ##  $ Make              : Factor w/ 93 levels "Acura Integra",..: 1 2 4 3 5 6 7 9 8 10 ...

위와 같이 하나의 데이터에도 많은 데이터 형태가 있음을 볼 수 있다. <br> 데이터 형태를 잘 알아두어야 <br> 1.각 데이터
속성에 맞는 함수를 적용가능<br> 2.데이터별 속성이 잘못 들어간 경우 바로잡기 가능 (숫자형이 factor 라든지…)

``` r
# as.factor(데이터) : 데이터를 factor 로 변환해준다.
x <- c('A','B','C')
factor_x <- as.factor(x)
str(factor_x) # level이 생긴 factor 형태가 된 것을 볼 수 있다.
```

    ##  Factor w/ 3 levels "A","B","C": 1 2 3

``` r
# as.numeric(데이터) : 데이터를 숫자로 변환한다.
x <- c('4','5','10')
str(x) # chr 의 데이터 tpye
```

    ##  chr [1:3] "4" "5" "10"

``` r
numeric_x <- as.numeric(x)
str(numeric_x) # chr -> num 으로 데이터 type 이 바뀐것을 볼 수 있다.
```

    ##  num [1:3] 4 5 10

``` r
# as.character(데이터) : 데이터를 chr 로 변환
as.character(3.14)
```

    ## [1] "3.14"

``` r
# as.vector(데이터) : 데이터를 vector 로 변환
as.vector('C')
```

    ## [1] "C"

``` r
# as.logical(데이터) : logic 값으로 변환
as.logical(3.42) # 이때에 0 일때에만 False 를 내보내고 나머지 경우는 True 를 나타낸다. 
```

    ## [1] TRUE

``` r
as.integer(3.2)
```

    ## [1] 3

``` r
as.numeric('go') # 바꿀수 없는 경우 에러가 뜬다.
```

    ## Warning: 강제형변환에 의해 생성된 NA 입니다

    ## [1] NA

``` r
as.character(100)
```

    ## [1] "100"

``` r
as.numeric(FALSE) # FALSE 인 경우 0 
```

    ## [1] 0
