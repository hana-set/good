---
title:  "ggplot2 기초문법"
excerpt: "ggplot2 의 기초 문법을 알아봅시다."
categories:
  - R_Visualization
tags:
  - 시각화
last_modified_at: 2021-01-17

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: false
---

{% highlight r %}
library('ggplot2')
{% endhighlight %}
# ggplot2 의 문법 및 기초
ggplot2 는 시각화 그래프 패키지이다. <br>
ggplot 은 신규 요소를 하나씩 쌓아가는 방식으로 그래프를 만든다. <br>
qplot 도 있으나, 그것은 ggplot 과 거의 유사하여 여기서는 ggplot 만 소개하겠다. <br>
ggplot 의 구성요소는 다음과 같이 5가지 이다. <br>

- data frame (데이터) <br>
- 미학요소(aesthetics)(aes)(Mapping) (그래프 크기,색상 등을 데이터와 Mapping)  <br>
- 기하학적 요소(geometries)(geoms) (점,선,모양) 즉 그래프형태 <br>
- 통계적 처리(stats) <br>
- 그래프의 배치(Position) <br> 


{% highlight r %}
ggplot(data=mtcars, # 데이터 설정
       aes(x=disp,y=mpg))+  # x 는 disp , y 는 mpg 로 설정
  geom_point(aes(size=hp,color=wt),stat='identity') # size 는 hp 기준 , color 는 wt값 기준
{% endhighlight %}

![plot of chunk unnamed-chunk-2](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-2-1.png)
위 코드를 보자. <br>

- 데이터는 mtcars  <br>
- mapping이 aes의 (x=..y=..) 로 이루어지고 있다. <br>
- 기하학적 요소는 geom 으로 생성(geom_point : 산점도) <br>
- Position과 stat 기본값 (identity) 사용 <br>


{% highlight r %}
ggplot(data = iris,
       aes(x = Sepal.Length, y = Sepal.Width, color = Species))+
  # note color 와  colour 는 같다. 혼용해서 사용한다고 한다. 
  geom_point(size=3)+
  # size 를 크게 한다. 
  geom_smooth(formula = y~x) # smooth 를 통해서 추세선을 긋는다.
{% endhighlight %}

![plot of chunk unnamed-chunk-3](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-3-1.png)


{% highlight r %}
library(ggplot2)
ggplot(data = BOD, aes(x=Time, y=demand)) +
    geom_bar(stat='identity') # geom 에서 point 말고 barplot 을 이용할 수 있다.
{% endhighlight %}

![plot of chunk unnamed-chunk-4](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-4-1.png)


{% highlight r %}
ggplot(sleep, aes(ID, extra, fill=group))+
    geom_bar(stat='identity', position = 'dodge') # barplot 에서 position 의 변화를 주었다.
{% endhighlight %}

![plot of chunk unnamed-chunk-5](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-5-1.png)

# ggplot 구성요소 
이제 어느정도 예시를 통해서 ggplot 의 기초 동작을 알아보았다. <br>
이제 ggplot cheet sheet(r studio) 의 내용을 기초로 각각의 구성요소들에 대해서 알아보자.<br>
ggplot2 그래프는  Layer + Scale + Coordinate System + (Facet) + (Guide) 순으로  쌓인다. <br>

## aes
plot 안에서 aes 를 사용하여(mapping) 데이터와 그래프 연결

{% highlight r %}
ggplot(data=mtcars, mapping = aes(x=hp, y=mpg)) + 
    geom_point() +
    geom_smooth()
{% endhighlight %}

![plot of chunk unnamed-chunk-6](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-6-1.png)

만약 smotthing 곡선과 point 자체의 color,size 등을 수정하고싶다면 aes 가 아니라 geom 위에서 수정해야한다. 

{% highlight r %}
ggplot(data=mtcars, mapping = aes(x=hp, y=mpg)) + 
    geom_point(color="green") +
    geom_smooth(color="green")
{% endhighlight %}

![plot of chunk unnamed-chunk-7](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-7-1.png)

만약 아래와 같이 aes 로 색을 지정하려 하면 설정이 안된다.

{% highlight r %}
ggplot(data=mtcars, mapping = aes(x=hp, y=mpg)) + 
    geom_point(mapping = aes(color="green")) +
    geom_smooth(mapping = aes(color="green"))
{% endhighlight %}

![plot of chunk unnamed-chunk-8](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-8-1.png)

geom 안에서 color 설정으로, cyl 마다 다른 추이를 볼 수 있음

{% highlight r %}
ggplot(data=mtcars, mapping = aes(x=hp, y=mpg)) + 
    geom_point(mapping = aes(color=as.factor(cyl))) +
    geom_smooth()
{% endhighlight %}

![plot of chunk unnamed-chunk-9](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-9-1.png)



## Stat
stat(statistical transformation) 은 주어진 데이터셋을 geom 이 활용하기 편하도록 데이터를 변환하는 역할을 한다. <br>
예시로 히스토그램을 그리려면 해당 bin 에 속할 수 있도록 통계적으로 집계가 필요하다. 이런 통계적 연산을 담당하는 알고리즘이 Stat 이다.(이때 stat은 count이다.) <br>
각각의 geom 에는 알맞은 stat 이 default 로 되어있다. <br>

<br>

{% highlight r %}
HR = read.csv('./data/HR.csv')
HR$left = as.factor(HR$left)
HR$salary = factor(HR$salary,levels = c("low","medium","high"))
{% endhighlight %}

# 테마 

{% highlight r %}
library(ggthemes)
Graph = ggplot(HR,aes(x=salary)) +  
  geom_bar(aes(fill=salary)) 

Graph + theme_bw() + ggtitle("Theme_bw") 
{% endhighlight %}

![plot of chunk unnamed-chunk-12](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-12-1.png)

{% highlight r %}
Graph + theme_classic() + ggtitle("Theme_classic") 
{% endhighlight %}

![plot of chunk unnamed-chunk-12](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-12-2.png)

{% highlight r %}
Graph + theme_dark() + ggtitle("Theme_dark") 
{% endhighlight %}

![plot of chunk unnamed-chunk-12](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-12-3.png)

{% highlight r %}
Graph + theme_light() + ggtitle("Theme_light")  
{% endhighlight %}

![plot of chunk unnamed-chunk-12](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-12-4.png)

{% highlight r %}
Graph + theme_linedraw() + ggtitle("Theme_linedraw") 
{% endhighlight %}

![plot of chunk unnamed-chunk-12](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-12-5.png)

{% highlight r %}
Graph + theme_minimal() + ggtitle("Theme_minimal") 
{% endhighlight %}

![plot of chunk unnamed-chunk-12](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-12-6.png)

{% highlight r %}
Graph + theme_test() + ggtitle("Theme_test") 
{% endhighlight %}

![plot of chunk unnamed-chunk-12](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-12-7.png)

{% highlight r %}
Graph + theme_void() + ggtitle("Theme_vold") 
{% endhighlight %}

![plot of chunk unnamed-chunk-12](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-12-8.png)

# 범례

## 범례제목 및 색
- **fill** : 색을 채우는 개념
- **col** : 겉 형태의 색을 바꿈(테두리,선,점..)

{% highlight r %}
ggplot(HR,aes(x=salary)) +  
  geom_bar(aes(fill=salary)) +
  theme_bw() +
  labs(fill = "범례 제목 수정(fill)")
{% endhighlight %}

![plot of chunk unnamed-chunk-13](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-13-1.png)

{% highlight r %}
ggplot(HR,aes(x = salary)) +  
  geom_bar(aes(col = salary)) +
  theme_bw() +
  labs(col = "범례 제목 수정(col)")
{% endhighlight %}

![plot of chunk unnamed-chunk-13](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-13-2.png)

## 범례위치

{% highlight r %}
Graph + theme(legend.position = "top")
{% endhighlight %}

![plot of chunk unnamed-chunk-14](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-14-1.png)

{% highlight r %}
Graph + theme(legend.position = "bottom")
{% endhighlight %}

![plot of chunk unnamed-chunk-14](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-14-2.png)

{% highlight r %}
Graph + theme(legend.position = c(0.9,0.7)) # 비율에 맞는 위치
{% endhighlight %}

![plot of chunk unnamed-chunk-14](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-14-3.png)

{% highlight r %}
Graph + theme(legend.position = 'none') # 위치 없음
{% endhighlight %}

![plot of chunk unnamed-chunk-14](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-14-4.png)

## 범례 테두리
margin 을 1,1,1,1 로 줌으로써 테두리를 만들 수 있다.

{% highlight r %}
Graph + theme(legend.position = "bottom")
{% endhighlight %}

![plot of chunk unnamed-chunk-15](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-15-1.png)

{% highlight r %}
Graph + theme(legend.position = "bottom",
              legend.box.background = element_rect(),
              legend.box.margin = margin(1, 1, 1, 1)) 
{% endhighlight %}

![plot of chunk unnamed-chunk-15](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-15-2.png)

# 축
축의 경우 제일 먼저 체크해야 하는것은 축에 설정된 변수가 conti 인지 discrete 인지이다. <br>

- **이산형** : scale_x_discrete()<br>
- **연속형** : scale_x_discrete()<br>

## 축 이름,단위

{% highlight r %}
ggplot(HR,aes(x = salary)) +  
  geom_bar(aes(fill = salary)) + #barplot 생성 
  theme_bw() + # 테마 붙이기 
  scale_x_discrete(expand =  c(0,0), labels = c("하","중","상")) + # discrete 한 x축 
  scale_y_continuous(expand = c(0,0),breaks = seq(0,8000,by = 1000)) # 1000 단위로 구분되는 y 축
{% endhighlight %}

![plot of chunk unnamed-chunk-16](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-16-1.png)

{% highlight r %}
ggplot(HR,aes(x = salary)) +  
  geom_bar(aes(fill = salary)) + # salary 로 구분되는 barchart
  theme_bw() +
  scale_x_discrete(expand =  c(0,0), labels = c("하","중","상")) +
  scale_y_continuous(expand = c(0,0),breaks = seq(0,8000,by = 1000)) +
  scale_fill_discrete(labels = c("하","중","상")) # 라벨의 변경
{% endhighlight %}

![plot of chunk unnamed-chunk-16](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-16-2.png)

## 축 범위

{% highlight r %}
ggplot(HR,aes(x = salary)) +  
  geom_bar(aes(fill = salary)) +
  theme_bw() +
  ylim(0,5000) # ylim 을 통해서 축의 범위 조절 가능
{% endhighlight %}

![plot of chunk unnamed-chunk-17](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-17-1.png)

{% highlight r %}
# 이떄 범위를 넘어서게 된다면, 넘는 범위의 값은 짤린다.

ggplot(HR,aes(x = salary)) +  
  geom_bar(aes(fill = salary)) +
  theme_bw() +
  ylim(0,13000)
{% endhighlight %}

![plot of chunk unnamed-chunk-17](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-17-2.png)

## 축 색깔
- scale_fill-manual : 사용자가 임의로 색을 입힌다. <br>
- alpha : 투명도 <br>

{% highlight r %}
ggplot(HR,aes(x = salary)) +  
  geom_bar(aes(fill = salary)) +
  theme_bw() +
  scale_fill_manual(values = c('red','royalblue','tan')) 
{% endhighlight %}

![plot of chunk unnamed-chunk-18](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-18-1.png)

# 그래프 배치
- coord_flip() : x,y 축의 위치를 대칭이동
- facet_wrap() : 분할하고픈 변수 지정 뒤, ncol 로 열 몇개로 나열할지 결정

{% highlight r %}
ggplot(HR,aes(x = salary)) +  
  geom_bar(aes(fill = salary), alpha = 0.4) +
  theme_bw() +
  scale_fill_manual(values = c('red','royalblue','tan')) +
  coord_flip()
{% endhighlight %}

![plot of chunk unnamed-chunk-19](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-19-1.png)

{% highlight r %}
ggplot(HR,aes(x = salary)) +  
  geom_bar(aes(fill = salary)) +
  theme_bw() +
  scale_fill_manual(values = c('red','royalblue','tan'))  +
  guides(fill = FALSE) + 
  facet_wrap(~time_spend_company,ncol = 2) 
{% endhighlight %}

![plot of chunk unnamed-chunk-19](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-19-2.png)

# 글자크기, 각도 

{% highlight r %}
ggplot(HR,aes(x = salary)) +  
  geom_bar(aes(fill = salary)) +
  theme_bw() +
  scale_fill_manual(values = c('red','royalblue','tan'))  +
  coord_flip() +
  theme(legend.position = 'none',
        axis.text.x = element_text(size = 15,angle = 90),
        axis.text.y = element_text(size = 15),
        legend.text = element_text(size = 15))
{% endhighlight %}

![plot of chunk unnamed-chunk-20](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-20-1.png)

# Coordinate Sytem 

{% highlight r %}
d <- ggplot(mpg, aes(fl))
r <- d + geom_bar() ; r
{% endhighlight %}

![plot of chunk unnamed-chunk-21](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-21-1.png)

## default

{% highlight r %}
r + coord_cartesian(xlim = c(0, 5))
{% endhighlight %}

![plot of chunk unnamed-chunk-22](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-22-1.png)

## 그래프 비율 조절 
가로축과 세로축의 비율 설정 <br>
현재 세로는 200 정도, 가로는 5(discrete 으로 범주가 5개) 이므로 정사각형 모양을 하려면 비율은 0.025 정도가 되어야 한다.

{% highlight r %}
r + coord_fixed(ratio = 0.025)
{% endhighlight %}

![plot of chunk unnamed-chunk-23](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-23-1.png)

## x,y 축 뒤집기

{% highlight r %}
r + coord_flip()
{% endhighlight %}

![plot of chunk unnamed-chunk-24](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-24-1.png)

## polar coordinate

{% highlight r %}
r + coord_polar(theta = "x", direction=1 ) 
{% endhighlight %}

![plot of chunk unnamed-chunk-25](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-25-1.png)

## coordinate trnas

{% highlight r %}
r + coord_trans(y = "sqrt") # y 에 sqrt 를 먹임
{% endhighlight %}

![plot of chunk unnamed-chunk-26](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-26-1.png)

{% highlight r %}
ggplot(diamonds, aes(carat, price)) +
  geom_point() +
  coord_trans(x = "log10", y = "log10") # x,y 에 변환울 곰
{% endhighlight %}

![plot of chunk unnamed-chunk-26](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-26-2.png)

# Position 
포지션 조절해서 , geom 생성시 어떤 배열로 그래프를 놓을지 설정한다. <br>

## dodge
dodge 의 경우 element 들을 옆으로 주루룩 새워놓는다.

{% highlight r %}
s <- ggplot(mpg, aes(fl, fill = drv)) 
s + geom_bar(position = "dodge")
{% endhighlight %}

![plot of chunk unnamed-chunk-27](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-27-1.png)

## fill
fill 은 같은 범주안에서 각자 비율대로 채워진다.

{% highlight r %}
s + geom_bar(position = "fill")
{% endhighlight %}

![plot of chunk unnamed-chunk-28](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-28-1.png)

## jitter
jitter 의 경우 x,y 좌표를 흩뿌린다.

{% highlight r %}
e <- ggplot(mpg, aes(cty, hwy))
e + geom_point(position = "jitter")
{% endhighlight %}

![plot of chunk unnamed-chunk-29](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-29-1.png)

## stack
stack 의 경우, 값들이 위로 쌓여 올라간다.

{% highlight r %}
s + geom_bar(position = "stack")
{% endhighlight %}

![plot of chunk unnamed-chunk-30](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-30-1.png)

# faceting
fl 이라는 column 에 근거해서 column 별로 그래프 나눠그림

{% highlight r %}
t <- ggplot(mpg, aes(cty, hwy)) + geom_point()
t + facet_grid(. ~ fl)
{% endhighlight %}

![plot of chunk unnamed-chunk-31](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-31-1.png)

row 별로 나눠 그리기

{% highlight r %}
t + facet_grid(year ~ .)
{% endhighlight %}

![plot of chunk unnamed-chunk-32](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-32-1.png)

row,col 두개로 나누기

{% highlight r %}
t + facet_grid(year ~ fl)
{% endhighlight %}

![plot of chunk unnamed-chunk-33](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-33-1.png)

사각형 layout 에 wrap 하기

{% highlight r %}
t + facet_wrap(~ fl)
{% endhighlight %}

![plot of chunk unnamed-chunk-34](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-34-1.png)

scale 과 함께 사용하여, 각 축 범위의 limit 제한을 없앤 그래프<br>
scale 이 없다면, 모두 같은 scale 을 사용하게 된다. <br>
labeller 를 넣어서, 각 그래프의 label 을 제목으로 표시해주었다.

{% highlight r %}
t + facet_grid(drv ~ fl, scales = "free",labeller = label_both)
{% endhighlight %}

![plot of chunk unnamed-chunk-35](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-35-1.png)

# 제목 및 캡션

{% highlight r %}
t + labs( x = "x 축의 이름", y = "y 축 이름",
title ="제일 큰 제목",
subtitle = "부제목 달기",
caption = "왼쪽 아래에 캡션 달기") 
{% endhighlight %}

![plot of chunk unnamed-chunk-36](/assets/images/Vis_ggplot2_elementary/unnamed-chunk-36-1.png)

# Reference
- https://wikidocs.net/73434 <br>
- ggplot2 cheat sheet rstudio <br>
- https://m.blog.naver.com/definitice/221128096345 <br>

