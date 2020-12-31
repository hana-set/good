---
title: "[Kaggle #1]Real or Not? NLP with Disaster Tweets-(1)"
categories: 
  - Kaggle
last_modified_at: 2020-02-18 12:00:00
toc: false #Table of Contents
comments: true
use_math: false # MathJax On
---

블로그 창시 이래, 여러개의 카테고리를 두었으나. 아직까지 하나의 게시물도 오르지 못한 카테고리가 있다.

바로 오늘 포스트가 속할 카테고리인 `Kaggle`이 그 주인공이다.

<br>

## Kaggle 이란?

> 캐글(Kaggle)은 2010년 설립된 예측모델 및 분석 대회 플랫폼이다. 
>
> 기업 및 단체에서 데이터와 해결과제를 등록하면, 데이터 과학자들이 이를 해결하는 모델을 개발하고 경쟁한다. 
> 
> 2017년 3월 구글에 인수되었다.
>
> [출처: 위키백과,   캐글](https://ko.wikipedia.org/wiki/%EC%BA%90%EA%B8%80)
<br>

Kaggle에 대한 장황한 설명을 기대하면 위키백과에 검색해보니 위처럼 매우 간결한 정의가 나타난다.

기대가 틀어진 것에 대한 약간의 실망감을 안고 정의된 문장을 읽어보니 사실 캐글을 설명하는데 중요한 내용이 전부 녹아있다.

먼저 Kaggle은 **데이터 분석 대회 플랫폼**이다.

<br>
<center><img src="/assets/images/200218/000.jpg" width="500" ></center>
<center><font size="3em">자신의 실력을 증명할 수 있는 신성한 대회의 장 - 토리야마 아키라, '드래곤볼'</font></center>
<br>

약간의 익살을 붙여본다면, 말그대로 **데이터분석가 세계의 천하제일무술대회**인 셈이다.

그렇기에 Kaggle이란 플랫폼을 통해 데이터분석가들은 

>
> 1. 자신의 이름을 세상에 떨치기위해 ~~라고쓰고 실상은 몸값을 올리기위해~~
> 2. 또는 Kaggle의 데이터를 가지고 자신의 실력향상을 위해
> 3. 다 필요없고 기업에서 내건 상금을 위해
> 

등등 다양한 동기를 가지고 접근하게된다.

나는 참고로 위에서 2번에 큰 의미를 두고있다.
~~(흐..흥! 딱히 상금을 받을만큼의 자신이 없어서가 아니라구..!)~~
<br>

-----

아 그리고, 구글에서 인수하였다는 점에서 유추하셨을지 모르겠지만 구글에서 제공하는 클라우드 서비스를 이용해 Jupyter Notebook 스타일의 분석환경을 계정별로 제공하고 있다.

이 말인 즉슨, 인터넷에 연결할 수 있는 환경만 있다면? 어디서든 분석을 자유롭게 돌려볼 수 있다는 의미다.

`여하튼` Kaggle은 대충 이런 플랫폼이다.

그리고 앞으로 내가 참여한 Kaggle의 Competetition들의 진척상황을 내키는대로 여기에 정리해볼 속셈이다.

대망의 첫번째 Competition은 바로...
<br>

## Real or Not? NLP with Disaster Tweets

<br>
<center><img src="/assets/images/200218/001.PNG" width="500" ></center>
<center><font size="3em"><a href="https://www.kaggle.com/c/nlp-getting-started">Real or Not? NLP with Disaster Tweets</a>, Kaggle</font></center>
<br>

처음 포스팅하게될 위 Competition은 **Twitter에 올라온 문자데이터를 바탕으로 실제 재난이 발생하였는지를 판별하는 대회**이다.

분석주제를 놓고보면 일단 **NLP(Natural Language Process)로 불리는 텍스트 분석**과 **재난상황에 대해 판별하는 Machine Learning 개발**이 예상된다.

하지만 오늘은 Kaggle의 포문을 여는 게시물로서 오늘 포스트 내용은 분석을 진행한 내용을 끄적거리기보다는 앞으로 Kaggle을 참여하며 진행되는 프로세스를 정리해보고자한다.
<br>

## Ehyun`s Kaggle 공부 프로세스 (ver 1.0)

<br>
<center><img src="/assets/images/200218/002.PNG" width="500" ></center>
<center><font size="3em">Ehyun`s Kaggle Developing Process ver1.0</font></center>
<br>

위에 나타난 대로 **`대회리뷰` > [ `Public 코드리뷰` <-반복-> `Private 코드작성` ] > `제출`** 의 과정을 거친다.

Kaggle은 공유정신을 지향하는 대회로써, 많은 선행 분석가들의 훌륭한 Public 코드들을 확인할 수 있다.

다른 분석가들의 코드를 리뷰하는 것만으로도 나의 실력 향상에 도움이 될 것이다.

한발 더 나아가, Public 코드들을 발판삼아 나의 분석코드인 Private 코드를 계속해서 업그레이드하며 실력을 체화하는 과정도 거치게된다.

그렇게 데이터를 핸들링하며 최종국면까지 접어들면, 최종적으로 Best Score를 기록한 버전의 결과물을 제출하고,  ~~나머지는 상금을 꿈꾸며 기도하도록 하자~~

내가 작성했던 Private 코드를 다듬어 공유할 수 있는 형태로 만들며 마무리하고자 한다.
<br>

-----

<br>
오늘은 Kaggle에 대해서, 앞으로 참가한 Kaggle 대회에 대한 나의 접근 프로세스에 대해서, 그리고 이번에 참여할 Competition에 대해서 개략적으로 알아보았다.

Kaggle은 데이터 분석능력을 향상시킬 수 있는 영양소를 잔뜩 머금고 있는 플랫폼인건 확실하다.

하지만 그 영양소를 온전히 내것으로 하기위해서는 부지런히 손가락을 움직여야 한다는 것 역시 확실하다.

마음을 다잡고 심혈을 기울이도록 노력해야겠다.
<br>
<br>
<br>

그럼 다음번에는 분석과정에서 발생하거나 결과물을 가지고 돌아오도록 하겠다.

이만 총총


