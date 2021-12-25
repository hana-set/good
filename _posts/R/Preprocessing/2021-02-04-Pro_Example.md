---
title:  "전처리 Example"
excerpt: "유용한 전처리 예시들에 대해 알아봅시다."
categories:
  - R_Preprocessing
tags:
  - 전처리
last_modified_at: 2021-02-04

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
---

# 년,월,일 나누기[substr]
아래와 같이 dataframe 에서 연월일이 붙어있는 경우가 있가. <br>
그런 경우에는 substr 을 이용하여 앞의 몇개만 떼어네서 데이터를 새로 만들 수 있다. <br>

{% highlight r %}
time <- c(20210101,20210302,20210401,20211230)
sell <- c(134,253,213,223)
df <- data.frame(time,sell) ;df 
{% endhighlight %}



{% highlight text %}
##       time sell
## 1 20210101  134
## 2 20210302  253
## 3 20210401  213
## 4 20211230  223
{% endhighlight %}



{% highlight r %}
df$year <- substr(df$time,1,4)
df$month <- substr(df$time,5,6)
df$day <- substr(df$time,7,8)
df
{% endhighlight %}



{% highlight text %}
##       time sell year month day
## 1 20210101  134 2021    01  01
## 2 20210302  253 2021    03  02
## 3 20210401  213 2021    04  01
## 4 20211230  223 2021    12  30
{% endhighlight %}
위와 같이 substr 을 이용하여 연,월,일을 만들어내었다.

# 문자형 벡터 붙이기[paste]
위에서 생성한 df 의 년,월,일에 각각 년,월,일 의 문자를 붙이고 싶다고 하자. <br>
그러면 이 떄 paste 를 이용해서 붙일 수 있다.

{% highlight r %}
df$year = paste(df$year,'년')
df$month = paste(df$month,'월')
df$day = paste(df$day,'일')
df
{% endhighlight %}



{% highlight text %}
##       time sell    year month   day
## 1 20210101  134 2021 년 01 월 01 일
## 2 20210302  253 2021 년 03 월 02 일
## 3 20210401  213 2021 년 04 월 01 일
## 4 20211230  223 2021 년 12 월 30 일
{% endhighlight %}

# 문자열 특정 문자 모두 지우기
이 dataset 에서 . 을 모두 지우고싶다고 하자.

{% highlight r %}
id <- c('a','b','c','d')
kg <- c(134.4,23.2,44.2,32.1)
df <- data.frame(id,kg) ; df
{% endhighlight %}



{% highlight text %}
##   id    kg
## 1  a 134.4
## 2  b  23.2
## 3  c  44.2
## 4  d  32.1
{% endhighlight %}



{% highlight r %}
df$kg = gsub('.','',df$kg,fixed = TRUE)
df
{% endhighlight %}



{% highlight text %}
##   id   kg
## 1  a 1344
## 2  b  232
## 3  c  442
## 4  d  321
{% endhighlight %}


# 데이터 중복없이 unique 한 관측치만 선별하기 
duplicate 함수를 이용하여 중복되는 열은 제거할 수 있다. <br>
duplicated 는 중복값이 아닐때에 false 를 출력하고, 중복값이면(이전에 나왔으면) True 를 출력한다.


{% highlight r %}
a1 <- rep(1:10, each=2)
a2 <- rep(c(1,3,5,7,9),each=4)
a3 <- c(1,1,1,1,3,3,3,3,5,5,6,6,7,7,8,8,9,10,11,12)
df <- data.frame(cbind(a1,a2,a3)) ; df
{% endhighlight %}



{% highlight text %}
##    a1 a2 a3
## 1   1  1  1
## 2   1  1  1
## 3   2  1  1
## 4   2  1  1
## 5   3  3  3
## 6   3  3  3
## 7   4  3  3
## 8   4  3  3
## 9   5  5  5
## 10  5  5  5
## 11  6  5  6
## 12  6  5  6
## 13  7  7  7
## 14  7  7  7
## 15  8  7  8
## 16  8  7  8
## 17  9  9  9
## 18  9  9 10
## 19 10  9 11
## 20 10  9 12
{% endhighlight %}



{% highlight r %}
# a1,a2의 두개 변수를 기준으로 중복 체크 후 중복이있을때는 1개만선텍
unique(df[,c('a1','a2')]) # df[,c('a1','a2')] : 변수a1,a2만 선택
{% endhighlight %}



{% highlight text %}
##    a1 a2
## 1   1  1
## 3   2  1
## 5   3  3
## 7   4  3
## 9   5  5
## 11  6  5
## 13  7  7
## 15  8  7
## 17  9  9
## 19 10  9
{% endhighlight %}



{% highlight r %}
df_new = df[duplicated(df[,c('a1','a2')]),] ; df_new
{% endhighlight %}



{% highlight text %}
##    a1 a2 a3
## 2   1  1  1
## 4   2  1  1
## 6   3  3  3
## 8   4  3  3
## 10  5  5  5
## 12  6  5  6
## 14  7  7  7
## 16  8  7  8
## 18  9  9 10
## 20 10  9 12
{% endhighlight %}



{% highlight r %}
row.names(df_new) = NULL ; df_new # 꼭 index 를 초기화 하는 작업을 진행하자.
{% endhighlight %}



{% highlight text %}
##    a1 a2 a3
## 1   1  1  1
## 2   2  1  1
## 3   3  3  3
## 4   4  3  3
## 5   5  5  5
## 6   6  5  6
## 7   7  7  7
## 8   8  7  8
## 9   9  9 10
## 10 10  9 12
{% endhighlight %}
