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

## 2. 선형 분리 가능한 상황  

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
|조건 2|모든 라그랑제 승수가 0보다 크거나 같아야 한다. <br>$$\lambda_i \geq 0, i=1,...,n$$|$$\lambda_i \geq0, i=1,...,N$$|
|조건 3|모든 조건식에 대해 $$\lambda =0$$ 이거나 $$f_i(\theta)=0$$이 되어야 한다.<br> $$\lambda_i f_i(\theta)=0, i=1,...,n$$ |$$\lambda_i(t_i(W^TX_i + b)-1)=0, i=1,...,N$$|


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

![](http://i.imgur.com/bsLbs2y.png)
>$$\lambda$$을 위 식에서는 $$\alpha$$로 표기 하였음 

살펴 볼 점 
- 2차 목적 함수의 최대화 문제로 바뀜
- W,b를 푸는 문제가 아니라 라그랑제 승수를 푸는 문제로 바뀜
- 특징벡터 $$X_i$$가 두 특징벡터 내적($$X_i^TX_j$$)으로 바뀜
    - 선형 SVM을 비선형 SVM으로 확장하는데 결정적 역할 수행 

> 예제 문제 풀어 보기 : 패턴인식 오일석, 147p 예제 5.2

## 3. 선형 분리 불가능한 상황




## 4. 비선형 SVM 






