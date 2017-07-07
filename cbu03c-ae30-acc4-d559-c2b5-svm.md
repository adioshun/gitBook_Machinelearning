# Support Vector Machine (SVM)

![](http://i.imgur.com/QEoOAb9.png)

- Vladimir Vapnik이 제안

- 분류 오차를 줄이면서 동시에 여백을 최대로 하는 결정 경계(decision boundary)를 찾음
    - 여백 = 일반화 성능 강화 

- 이진 분류기(binary classifier)이나 M 분류로 확장 가능 

![](http://i.imgur.com/uF7mAZO.png)
[H2, H3 모두 분류 조건을 만족하나, H3가 더 일반성 높음]

- 여백(margin): 결정 경계와 가장 가까이에 있는 학습 데이터까지의 **거리**

- 서포트 벡터(support vector): 결정 경계로부터 가장 가까이에 있는 학습 데이터들, 결정 경계를 결정하게 되는 요소들

## 1. 개요



경계선는 평면(H), 데이터는 점(x) 

편면의 식 : $$h(x) = w_1x_1 + w_2x_2 + ..w_dx_d + b = w^T \cdot x + b =0 $$
- w : 가중치 
- x : 입력 
- b : 절편

경계선위의 임의의 벡터(a에서 x1)는 법선벡터(w)와 수직이므로 내적은 `0`이 된다. 
- $$w \cdot (x'-a) = 0 \rightarrow w^Tx' -w^Ta = 0$$



### 1.1 여백(Margin)을 계산 공식 유도  
![](http://i.imgur.com/gXlSIyR.png)

###### Step 1. $$x = x_p + r\frac{w}{\parallel w \parallel}$$
- x의 위치는 0점에서 $$x_p$$까지 이동 후 r만큼 이동한것  
- $$x_p$$ :  x를 프로젝션 하였을때의 값
- $$\frac{w}{\parallel w \parallel}$$: 단위 벡터 

###### Step 2. $$w^Tx = w^Tx_p + r\frac{w^Tw}{\parallel w \parallel}$$
- 첫 식에 양변에 $$w^T$$를 곱하면 아래식이 됨

###### Step 3. $$w^Tx = w^Tx_p + r\parallel w \parallel$$
- 위식에서 $$w^Tw=w^2$$이므로 변환 
- $$r\parallel w \parallel$$: norm, w벡터 크기 

###### Step 4. $$w^Tx + b = w^Tx_p + b + r\parallel w \parallel$$
- 위식에서 양변에 b를 더함 

###### Step 5. $$w^Tx + b = h(x) = 0 + r\parallel w \parallel$$
- $$x_p$$는 평면에 위치한 점 
- 즉, 평면의 식 공식$$w^Tx+b=0$$을 $$w^Tx_p+b$$에 대입

 
######  Step 6. 임의의 점(x)와 경계선의 거리(h) = r = 마진 

$$h(x) = 0 + r\parallel w \parallel $$
$$ r = \frac{h(x)}{\parallel w \parallel} $$


######  [예제] x가 0일떄 거리($$r_0$$)는?

$$r_0 = \frac{h(0)}{\parallel w \parallel} = \frac{b}{\parallel w \parallel}$$
- $$h(x) = w^T \cdot x + b $$

### 1.2 SVM 공식 유도

분류를 위한 초평면의 만족 조건 

![](http://i.imgur.com/hksvmUo.png)


#### A. 데이터를 둘로 나누어야 함   

초평면을 기준으로 0보다 크면 라벨($$t_i=1$$)
초평면을 기준으로 0보다 작으면 라벨($$t_i=-1$$)

#### B. 서포트 벡터까지의 거리가 1이 되어야 함   
h(x) = 1 

> 나머지 값(서포트 벡터가 아닌)은 1이상 : $$h(x) \geq1$$

## 2. 최적화 문제 풀기(Hard SVM)

### 2.1 라그랑즈 승수 
||원식|적용식|
|-|-|-|
|조건|![](http://i.imgur.com/8CgArpf.png)|![](http://i.imgur.com/RHvubC4.png)|
|||![](http://i.imgur.com/hVUcv5j.png)<br>라그랑주 함수 조건$$h(x) \leq 0$$과 맞추기 위해 $$t_ih(x_i) \geq 1을 $1-t_ih(x_i) \leq 0$$로변환 |
|라그랑즈함수|![](http://i.imgur.com/32dlWV4.png)|![](http://i.imgur.com/8ezIzm0.png)|


### 2.2 KKT 조건 

![](http://i.imgur.com/9GYM7av.png)

1. 라그랑즈 승수 조건 : 0보다 커야 함 
2. 부등식 제약 조건h(x) 0보다 작아햐 함(위에서 그래서 변환함)
3. 상보적 여유성(Complementary Slackness)조건 
 = 라그랑즈 승수 $$\times$$ 부등식 제약 조건 = 0



#### 2.3 쌍대 함수 

![](http://i.imgur.com/KPghOdX.png)

라그랑즈 함수를 w,b로 편미분해서 $$\alpha$$만 남아 있는 식으로 변경 

![](http://i.imgur.com/tno2YB0.png)
$$t_ix_i$$는 학습 데이터 이므로 $$\alpha$$만 남음 


#### 2.4 초평면 함수식에 적용 

쌍대 함수에서 구한 2개 식을 적용 

![](http://i.imgur.com/xLWP9zl.png)


#### 2.5 [정리] 

###### Step 1. 본 문제 -> 쌍대 문제 : 문제 복잡도 감소 

![](http://i.imgur.com/fBuUMGM.png)


###### Step 2. 쌍대함수 최대화 -> 쌍대함수 최소
방법 : 양변에 -1을 곱하기 

![](http://i.imgur.com/y3FqivG.png)


> 그냥 최대화 문제 풀면 안되나? 알고리즘들이 최소화 문제 대상이라 그런가 (???)

###### Step 3. 이차식 계획법 

쌍대함수 최소화 문제는 $$\alpha$$입장에서 보면 2차식 문제 

![](http://i.imgur.com/z9fMKwW.png)

> Python의 solvers.qp()라이브러리로 해결 가능 

## 3. 최적화 문제 풀기(Soft SVM)
선형 분리가 불가한 문제의 SVM

슬랙변수를 이용하여 문제 풀이 

## 4. 비선형 svm 

데이터의 고차원 사상(high-dimensional mapping)
- 데이터를 고차원의 사상하면 선형 분리 가능

![](http://i.imgur.com/H1kKMj2.png)

고차원 변환의 문제점
- 차원의 저주(curse of dimensionality) 문제 발생
- 테스트 데이터에 대한 일반화(generalization) 능력 저하 가능
 - SVM은 여백(margin) 최대화를 통해 일반화 능력 유지
- 계산 비용 증가
 - SVM은 커널 트릭(kernel trick) 사용으로 해결

### 4.1 커널 트릭 

---
