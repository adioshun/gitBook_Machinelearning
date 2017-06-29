

# 개념수업 미분이란무엇인가
> 출처 : [개념수업 미분이란무엇인가](https://www.youtube.com/watch?v=2JvfRLgcmUI)



## 1. 개요



![](http://i.imgur.com/KO08KsE.png)

미분한다 = (한점에서의) 기울기를 구한다. = $$f\prime$$

기울기 구하는법 
- 두점의 기울기(평균 변화율) : $$ \frac{f(x)-f(a)}{x-a} $$
- 한점의 기울기(순간 변화율) : $$ \lim_{x \rightarrow a}\frac{f(x)-f(a)}{x-a} = f\prime(a)$$

> 두점(x, a)의 사이를 아주 가깝게 하여 x=a로 만듬

## 2. 표현법/식
![](http://i.imgur.com/ed9FGRk.png)

- h를 이동거리(간격)으로 할때 : $$a+h  \Leftarrow 많이 쓰임$$  
- 변화량 x로 할때 : $$a+\Delta{x} $$
- 변활율 $$\frac{x}{y}$$로 할때 : $$\frac{\Delta x}{\Delta y} \Rightarrow \lim_{\Delta x \rightarrow 0}\frac{\Delta x}{\Delta y}\Rightarrow \frac{d x}{d y} $$ 


> $$\Delta$$ : Difference 의미(변화양), Delta라 읽음,

원래   $$\Delta = d $$는 같은것이지만 필요에 의해 둘을 다른 의미로 사용 
- $$\Delta$$ :  변화량
- $$\ d$$ : $$\lim_{\Delta x \rightarrow 0}되 \Delta $$

## 3. $$\frac{dy}{dx} = \frac{d}{dx}y$$에 대한 고찰 

읽는법
- dx분에 dy
- dx에 대한 dy (일반적)

의미 
- $$\frac{dy}{dx}$$: (dx에 대해) y를 미분 하라.
- y에 대한 식이다.  eg. $$y = x^3 + 2x^2$$
 

계산법

|![](http://i.imgur.com/ruN0L8U.png)|![](http://i.imgur.com/pgiXrEh.png)|
|-|-|
|![](http://i.imgur.com/KQZOn04.png)|![](http://i.imgur.com/rnHPMzf.png)|

지수의 숫자를 앞으로 내리고 지수에서 그 대가로 1을 뺀다. 상수는 0이 된다. 

> 출처 : [waylight3](http://waylight3.blog.me/220221644620)

# 지수 함수의 미분 
> 출처 : [지수 로그 함수의 미분 로피탈 공식](https://youtu.be/si6ckKuXNBo)



미분 = 원식 * 미분식 * ln a

$$y = a^{x{^2}+2x+3} \Rightarrow y\prime = a^{x{^2}+2x+3} \cdot (2x+2)\cdot \ln a$$ 


# 지수 로그 함수의 미분 

미분 = 원식 * 미분식 * ln a

$$y=e^x \Rightarrow y\prime = e^x$$

$$y=e^{x^2+x} \Rightarrow y\prime = e^{x^2+x} \cdot (2x+1) $$

> 미분을 했어도 값이 줄지 않음, $$\ln$$=1이어서 생략

## 로그 함수의 미분 

$$ y = \log_a x \Rightarrow y\prime = \frac{1}{(x)\ln(a)}$$

로그 이후의 값으로 1/n을 만들고, 로그 밑 값으로 ln a만듬

$$ y = \log_a (x^2+x) \Rightarrow y\prime = \frac{1}{(x^2+x)\cdot \ln (a)} $$





