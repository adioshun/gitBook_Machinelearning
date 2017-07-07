# SVM

- 기존 분류기 : 기존 방법들은 오류율을 최소화
- SVM 분류기 : 부류 사이에 존재하는 margin(여백)을 최대화 하여 일반화 능력을 극대화

주요 고려 사항 

- margin 이라는 개념을 어떻게 공식화 할 것인가?

- 여백을 최대로 하는 결정 초평면은 어떻게 찾아낼 것인가?


## 1. 결정 초평면 

### 1.1 결정 초평면 개요
- 정의 : 두 공간으로 나누는 평면

- 수식 : $$d(x) = W^tX + b = 0 $$
    - X : 샘플을 나타내는 특징 텍터
    - w,b : 결정 초평면을 정의 하는 매개  변수 
    
### 1.2 결정 초평면 특성

1. d(x) > 0 과 d(x)<0 에 따라 두 영역으로 나누어짐 

2. w, b에 상수 c를 곱하여도 같은 초평면을 나타냄

3. w는 초평면의 법선벡터로 초평면의 방향을 나타냄, b는 위치를 나타냄

4. 임의의 점 x에서 초평면까지의 거리는 $$h=\frac{\mid d(x) \mid}{\parallel w \parallel}$$


###### [참고] 점$$(x_1, y_1)$$과 직선 $$ax + by +c =d$$ 사이의 거리 = d = $$\frac{|ax_1 + by_1 +c|}{\sqrt{a^2 + b^2}}$$

## 2. Hard SVM (선형 분리 가능한 상황)

###### Step 1. 목표 정의 

훈련 집합 $$X = (값, 라벨) = {(x_1,t_1),(x_2,t_2),...(x_N,t_N)}$$ 일때 

|조건 1|$$x_i가 \omega_1에 속하면 t_i=+1$$|$$W^TX_i + b \geq +1, \forall X_i \in \omega_1) $$|
|-|-|
|조건 2|$$x_i가 \omega_2에 속하면 t_i=-1$$|$$W^TX_i + b \leq -1, \forall X_i \in \omega_2) $$|
|목표| 여백 최대화 |$$h=\frac{\mid d(x) \mid}{\parallel w \parallel} \rightarrow 2h=\frac{2\mid d(x) \mid}{\parallel w \parallel} =\frac{2}{\parallel w \parallel}$$|
> h에 2는 왜 곱하지???

###### Step 2. 조건부 최적화 문제로 간소화 

- 조건 : $$t_i(W^TX_i + b)-1 \geq0, i=1,...,N$$

- 최적화 : $$J(W) = \frac{1}{2} \parallel W \parallel ^2 $$ 
    - $$\frac{1}{\parallel W \parallel}$$의 최대화는 $$ \parallel W \parallel ^2$$ 의 최소화와 같음 
    - 계수 $$\frac{1}{2}$$는 계산 편리를 위해 추가 


> J(W)가 2차 항만을 가지므로 볼록함수이다. 즉, 지역(Local) 최적점에 빠지지 않는다. 

###### Step 3. 라그랑제 승수로 정의

조건부 최적화는 `라그랑제 승수`로 도입하여 푼다. 

|$$L(\theta, \lambda) = J(\theta) - \sum^n_{i=1}\lambda_i f_i(\theta) $$|
|-|

$$

L(W,b,\lambda) = \frac{1}{2} \parallel W \parallel ^2 - \sum^N_{i=1} \lambda_i(t_i(W^TX_i + b)-1) 

$$

 
###### Step 3. KKT조건으로 문제 풀이 

부등식 조건부 최적화 문제는  `KKT 조건`으로 푼다. 

||Karush-Kuhn-Tucker(KKT) 3 조건 |문제풀이|
|-|-|-|
|조건 1|라그랑제 함수를 미분한식이 0이 되어야 한다.<br> $$\frac{\partial L(\theta, \lambda)}{\partial \theta}=0$$|$$\frac{\partial L(W, b, \lambda)}{\partial W}=0 \rightarrow W = \sum^N_{i=1} \lambda_it_iX_i$$|
|||$$\frac{\partial L(W, b, \lambda)}{\partial b}=0 \rightarrow \sum^N_{i=1} \lambda_it_i=0$$|
|조건 2|모든 라그랑제 승수가 0보다 크거나 같아야 한다. <br>$$\lambda_i \geq 0, i=1,...,n$$|$$\lambda_i \geq0$$ <br> $$i=1,...,N$$|
|조건 3|모든 조건식에 대해 $$\lambda =0$$ 이거나 $$f_i(\theta)=0$$이 되어야 한다.<br> $$\lambda_i f_i(\theta)=0, i=1,...,n$$ |$$\lambda_i(t_i(W^TX_i + b)-1)=0$$ <br> $$ i=1,...,N$$|

[살펴볼점]
조건 3 : 모든 샘플에 대해 $$\lambda =0$$ 이거나 $$f_i(\theta)=0$$이 되어야 한다 
- $$\lambda \neq 0$$인 샘플은 $$t_i(W^TX_i + b)=1$$이어야 하는데 이들이 바로 Support Vector이다.
- $$\lambda = 0$$는 일반 샘플들이다. 
    
조건 1 : 매개 변수 w를 구할수 있다. 
- $$W = \sum^N_{i=1} \lambda_it_iX_i$$ 에서 $$t_i, X_i$$는 모두 훈련 데이터에서 얻을수 있음 
- 라그랑제 상수 $$\lambda$$만 구하면 W 를 구할수 있음 

조건 3 : 매개 변수 b를 구할수 있다. 
- $$\lambda \neq 0$$인 샘플은 $$t_i(W^TX_i + b)=1$$이어야 하므로
- $$t_i, X_i$$는 모두 훈련 데이터에서 얻을수 있음 
- [조건 1]로 W를 얻을 수 있음 


###### Step 4. wolfe Dual로 변형(간편화)
볼록성질을 만족하는 조건부 최적화 문제는 wolfe Dual로 변형 가능
- 부등식 조건 -> 등식 조건
- 최소화 -> 최대화 

||변경전(Step 2)|변경후|
|-|-|
|조건|$$t_i(W^TX_i + b)-1 \geq0, i=1,...,N$$|KKT조건|
|목표|$$J(W) = \frac{1}{2} \parallel W \parallel ^2 $$최소화|$$L(W,b,\lambda)=\frac{1}{2} \parallel W \parallel ^2 - \sum^N_{i=1} \lambda_i(t_i(W^TX_i + b)-1)$$최대화|

###### Step 5. 문제 풀이 

1. Step 3의 [조건 1]의 두 식을 $$ \frac{1}{2} \parallel W \parallel ^2 - \sum^N_{i=1} \lambda_i(t_i(W^TX_i + b)-1) $$ 에 대입 

2. W, b가 사라짐

3. 라그랑제 승수 $$\lambda$$만 남은 식을 $$\tilde L(\lambda)$$ 로 정의 

$$
\tilde{L}(\lambda) = \sum^N_{i=1} \lambda_i - \frac{1}{2}\sum^N_{i=1} \sum^N_{j=1}\lambda_i \lambda_j t_jt_jX_i^TX_j
$$

![](http://i.imgur.com/bsLbs2y.png)
>$$\lambda$$을 위 식에서는 $$\alpha$$로 표기 하였음 

살펴 볼 점 
- 2차 목적 함수의 최대화 문제로 바뀜
- W,b를 푸는 문제가 아니라 라그랑제 승수를 푸는 문제로 바뀜
- 특징벡터 $$X_i$$가 두 특징벡터 내적($$X_i^TX_j$$)으로 바뀜
    - 선형 SVM을 비선형 SVM으로 확장하는데 결정적 역할 수행 

> 예제 문제 풀어 보기 : 패턴인식 오일석, 147p 예제 5.2 [[초평면 거리 계산하기]](https://cpuu.postype.com/post/599833)

## 3. Soft SVM(선형 분리 불가능한 상황)

![](http://i.imgur.com/Etdi9Vd.png)
![](http://i.imgur.com/ALLBUA8.png)
$$\xi$$(Slack variable)

### 3.1 목표 정의 

아래를 동시에 만족하는 결정 초평면의 방향(W)를 찾아라 
- 여백을 될수 있는 한 크게 하며 (목적1)
- $$0 < \xi$$한 샘플수(경우 1,2)를 가능한 작게 한다 (목적2) 

$$

J(W,\xi) = \frac{1}{2}\parallel W \parallel^2 + C\sum^N_{i=1}\xi_i

$$
- 첫항 : 목적 1
- 두번쨰 항 : 목적 2
- C: 가중치 매개 변수 
    - C=0 :목적 2무시, 틀리는 샘플수에 개의치 않고 여백을 되 수 있는 대로 크게 한다
    - C=무한대 : 목적 2만 고려, 

###### Step 1. 목표 정의 

|조건 1|$$t_i(W^TX_i + b) \geq 1- \xi$$ <br> $$ i=1,...,N$$|
|-|-|
|조건 2|$$\xi_i \geq 0 $$ <br> i = 1,...,N|
|목표| $$J(W,\xi) = \frac{1}{2}\parallel W \parallel^2 + C\sum^N_{i=1}\xi_i$$ 최소화 |


###### Step 2. 라그랑제 승수 
> 조건이 2개 이므로 라그랑제 승수도 2개 

###### Step 3. KKT 조건 

###### Step 4. Wolfe 듀얼 변환 


## 4. 비선형 SVM 

커널(Kernel)을 사용함으로써 문제 해결 
- 커널 사용이 가능한 이유 : 유도 공식에 `벡터가 내적 형태`($$X_i^TX_j$$)로 존재 하여서 

원래 차원을 더 높은 공간으로 매핑하여 선형 분리가 가능하다. 
- 맵핑함수($$\Phi$$) 이용, $$\Phi: L \rightarrow H$$

### 4.1 커널함수 
- 두개의 벡터를 매개 변수를 취하며 K(X,Y)형태를 가진다. 

#### A. 커널 함수의 성질 

L공간 상의 두 벡터 x와 y를 매개 젼수로 갖는 커널 함수를 `K(x,Y)`라 하자. 

그러면 $$K(x,y)=\Phi(x) \cdot \Phi(y)$$를 만족하는 매핑함수 $$\Phi$$가 존재 하여야 한다. 

즉, 커널 함수의 값과 H공간으로 매핑된 두 점 $$\Phi(x) 와 \Phi(y)$$의 내적이 같아야 한다. 

#### B. 커널대치(Kernel substitution) Or 커널 트릭
어떤 수식이 벡터의 내적을 포함하고 있을 때 그 내적을 커널 함수로 대치 하여 계산 

|주요 개념: L공간에서 K()로 수행(실제 계산) = $$\Phi$$로 맵핑된 고차원 공간(H)에서 작업하는 효과 |
|-|
|- 효과 : 차원의 저주를 피할수 있음|

#### C. 커널 대치의 제약 및 특징 
- 가능한 연산이 `내적`밖에 없음
- `내적`을 사용하는 방법은 모두 커널 대치 기법을 도입 할수 있음 


#### D. 커널 대치를 이용한 목적함수 변경

|원식|$$\tilde{L}(\lambda) = \sum^N_{i=1} \lambda_i - \frac{1}{2}\sum^N_{i=1} \sum^N_{j=1}\lambda_i \lambda_j t_jt_j \cdot X_i^TX_j$$|
|-|-|
|맵핑함수|$$\tilde{L}(\lambda) = \sum^N_{i=1} \lambda_i - \frac{1}{2}\sum^N_{i=1} \sum^N_{j=1}\lambda_i \lambda_j t_jt_j \cdot \Phi(X_i)^T\Phi(X_j)$$|
|커널함수|$$\tilde{L}(\lambda) = \sum^N_{i=1} \lambda_i - \frac{1}{2}\sum^N_{i=1} \sum^N_{j=1}\lambda_i \lambda_j t_jt_j \cdot K(X_i,X_j)$$|


###### 커널 고르기 
- 어떤 양수 확정화의 대칭 함수든지 커널로 사용할 수 있다. 
    - 양수 확정화(Positive definite): 어떤 함수의 적분이든 양수로 만든다. 
- 커널들의 조합은 또 다른 커널을 만들어 낸다. 

- 일반적으로 사용되는 세 가지 다른 종류의 기저 함수가 있으며, 이에 대한 커널들이 존재 한다. 

|커널명|식|참고|
|-|-|-|
|선형커널|$$k(x,y)=xy+c$$||
|다항식커널|$$K(x,y) = (X^Ty+1)^x$$||
|가우시안커널,RBF커널|$$K(x,y) = \exp (-(x-y)^2/2\sigma^2) $$|방사기저함수 확장, 파라미터($$\sigma$$)|
|하이퍼탄젠트커널|$$K(x,y) = \tanh (kx^Ty - \delta) $$|시그모이드 함수, 파라미터($$k, \delta$$)|


- 커널 고르기
    - 밥닉 첼닉 차원(Vapnik-Chernik Demension)이론 적용
    - 대부분, 직접 모든 경우 시도 해보고 선택 
    
    
SVM이 사용하는 대표적 커널 함수 
![](http://i.imgur.com/eflzmwJ.png)






## 5. M 부류 SVM

### 5.1 1:M-1 방법 
- OVA(One versus All)

- 한 클래스당 한개씩의 총 n개의 판별 경계에 대해서 해당하는 클래스 라벨을 부여 하는 Winner takes all방식

- M 개의 이진 분류기를 사용하여 argmax(d(x)) 를 만족하는 부류를 찾는다.




### 5.2 1:1 방법 

- OVO(One Versus One)

- 모든 두 클래스간 $$\frac{n(n-1)}{2}$$개의 판별경계에 대해서 가장 많이 해당되는 클래스의 라벨을 부여하는 Max-wins 방식 

- M(M-1)/2 개의 이진 분류기를 사용하여 투표 방식으로 가장 많은 표를 얻은 부류로 분류한다.

- 투표 방식이라 신뢰도가 M-1에 비해 높지만, 신규 샘플이 들어 왔을 때 시간이 많이 걸린다.


## 6. SVM 회귀 
- 최소 오차 제곱을 사용

> 참고 : 알고리즘 중심의 머신러닝 가이드, 제이펍, 214P















































