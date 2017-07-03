

# 개념수업 미분이란무엇인가
> 출처 : [개념수업 미분이란무엇인가](https://www.youtube.com/watch?v=2JvfRLgcmUI)



## 1. 개요



![](http://i.imgur.com/KO08KsE.png)

미분한다 = (한점에서의) 기울기를 구한다. = $$f\prime$$

기울기 구하는법 
- 두점의 기울기(평균 변화율) : $$ \frac{f(x)-f(a)}{x-a} $$
- 한점의 기울기(순간 변화율) : $$ \lim_{x \rightarrow 0}\frac{f(x)-f(a)}{x-a} = f\prime(a)=\frac{d}{dx}f(x)$$

> 두점(x, a)의 사이를 아주 가깝게 하여 x=a로 만듬

## 2. 표현법/식
![](http://i.imgur.com/ed9FGRk.png)

- h를 이동거리(간격)으로 할때 : $$a+h  \Leftarrow 많이 쓰임$$  
- 변화량 x로 할때 : $$a+\Delta{x} $$
- 변활율 $$\frac{x}{y}$$로 할때 : $$\frac{\Delta x}{\Delta y} \Rightarrow \lim_{\Delta x \rightarrow 0}\frac{\Delta x}{\Delta y}\Rightarrow \frac{d x}{d y} $$ 


> $$\Delta$$ : Difference 의미(변화양), Delta라 읽음,

원래   $$\Delta = d $$는 같은것이지만 필요에 의해 둘을 다른 의미로 사용 
- $$\Delta$$ :  변화량
- $$\ d$$ : $$\lim_{\Delta x \rightarrow 0}된 \Delta $$

|기호|의미||
|-|-|-|
|$$\Delta$$|인접한 두 변수의 차이||
|$$d$$|두변수의 극미한차이||
|$$\partial$$|다변수함수에 대한 하나의 변수에 대한 변화량(편미분)||
|$$\bar d$$|통계적인 변수의 변화량||




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

### 3.1 곱의 미분 법칙
곱의 미분 = 한쪽만 미분한 것들의 합

$$(xy)\prime = x\prime y + y\prime x$$

### 3.2 나눗셈의 미분 법칙
$$(\frac{x}{y})\prime = \frac{x\prime y + y\prime x}{y^2}$$



### 3.2 $$\frac{1}{x}$$의 미분 

$$y = \frac{1}{x} = x^{-1} \rightarrow y\prime = -x^{-2}$$

### 3.3 지수함수, 자연로그 

$$y= e^x \rightarrow y\prime = e^x$$ (변화 없음)
$$y=\ln x \rightarrow y\prime = \frac{1}{x}$$
$$y=\ln{(ax+b)} \rightarrow y\prime = \frac{1}{(ax+b)}\times a$$


[참고] [미분 정리](https://ko.m.wikiversity.org/wiki/%ED%8F%AC%ED%84%B8:%EA%B3%A0%EB%93%B1%ED%95%99%EA%B5%90/%EC%88%98%ED%95%99/%EC%88%98%ED%95%99_II/%EA%B8%B0%EB%B3%B8%EC%A0%81%EC%9D%B8_%EB%AF%B8%EB%B6%84_%EA%B3%B5%EC%8B%9D#/editor/2)

## 4. 미분의 적용

### 4.1 지수 함수의 미분 
> 출처 : [지수 로그 함수의 미분 로피탈 공식](https://youtu.be/si6ckKuXNBo)



미분 = 원식 * 미분식 * ln a

$$y = a^{x{^2}+2x+3} \Rightarrow y\prime = a^{x{^2}+2x+3} \cdot (2x+2)\cdot \ln a$$ 



### 4.2 지수 로그 함수의 미분 

미분 = 원식 * 미분식 * ln a

$$y=e^x \Rightarrow y\prime = e^x$$

$$y=e^{x^2+x} \Rightarrow y\prime = e^{x^2+x} \cdot (2x+1) $$

> 미분을 했어도 값이 줄지 않음, $$\ln$$=1이어서 생략

### 4.3 로그 함수의 미분 

$$ y = \log_a x \Rightarrow y\prime = \frac{1}{(x)\ln(a)}$$

- 로그 이후의 값으로 1/n을 만들고, 로그 밑 값으로 ln a만듬

$$ y = \log_a (x^2+x) \Rightarrow y\prime = \frac{1}{(x^2+x)\cdot \ln (a)} $$



$$y = \ln x = \log_e x \Rightarrow y\prime = \frac{1}{x (\ln e) } = \frac{1}{x}$$
$$y = \ln (x^2+2x) \Rightarrow y\prime = \frac{1}{x^2+2x}$$

> ln은 쓰지 않음 

### 4.3 자연로그($$\log_e{x}$$) 함수의 미분

|자연로그 특징|
|-|
|$$e^x의 역함수$$|
|$$$$|
|$$$$|





> $$\ln$$=자연 로그= 실수(e)를 밑으로 하는 로그(log)



###### [참고] Log의 특징  



### 4.4 벡터 미분

 > 참고 : 머신러닝에서 딥러닝까지 별첨A.1, [다크 프로그래머](http://darkpgmr.tistory.com/141), [[추천]데이어트사이언스 스쿨](https://datascienceschool.net/view-notebook/8595892721714eb68be24727b5323778/), [영문교과서](http://www.atmos.washington.edu/~dennis/MatrixCalculus.pdf)


 
- 행렬 미분은 정확하게는 미분이 아닌 `편미분(partial derivative)`이지만 표현 편의상 미분이라고 표현 

- 데이터 분석은 대부분 스칼라(y=종속변수)를 벡터(x=독립변수)로 미분 하는 경우임 : $$\frac{\partial y}{\partial x_1},\frac{\partial y}{\partial x_2},\frac{\partial y}{\partial x_3}$$
- 결과는 그레이언트벡터(Gradient Vector)라고 하며 $$\triangledown y $$로 표기 
$$
\nabla y = 
\frac{\partial y}{\partial \mathbf{x}} =
\begin{bmatrix}
\dfrac{\partial y}{\partial x_1}\\
\dfrac{\partial y}{\partial x_2}\\
\vdots\\
\dfrac{\partial y}{\partial x_N}\\
\end{bmatrix}
$$

- 예시 

$$f(x,y)= 2x^2 + 6xy +7y^2 -26x -56y +107 $$

$$
\nabla f = 
\begin{bmatrix}
\dfrac{\partial f}{\partial x}\\
\dfrac{\partial f}{\partial y}\\
\end{bmatrix} =
\begin{bmatrix}
4x + 6y - 26\\
6x + 14y - 54\\
\end{bmatrix}
$$


##### [정리] 자주 쓰이는 벡터 미분 

![](http://i.imgur.com/HlzCWHP.png)
[증명보기](http://blog.naver.com/enewltlr/220918689039)








