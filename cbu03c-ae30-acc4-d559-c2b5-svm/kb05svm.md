# SVM

> 참고 : [Genuus 블로그](http://genius12.tistory.com/174)

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

- 최적화 : $$J(W) = \frac{1}{2} \parallel w \parallel ^2 $$ 
    - $$\frac{1}{\parallel w \parallel}$$의 최대화는 $$ \parallel w \parallel ^2$$ 의 최소화와 같음 
    - 계수 $$\frac{1}{2}$$는 계산 편리를 위해 추가 


> J(W)가 2차 항만을 가지므로 볼록함수이다. 즉, 지역(Local) 최적점에 빠지지 않는다. 

###### Step 3. 라그랑제 승수로 조건부 최적화 문제 풀이 

|$$L(\theta, \lambda) = J(\theta) - \sum^n_{i=1}\lambda_i f_i(\theta) $$|
|-|

$$

L(W,b,\alpha) = \frac{1}{2} \parallel w \parallel ^2 - \sum^N_{i=1} \alpha_i(t_i(W^TX_i + b)-1) 

$$

 




## 3. 선형 분리 불가능한 상황




## 4. 비선형 SVM 






