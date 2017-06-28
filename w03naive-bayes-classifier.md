# Naive Bayes Classifier

Naive = 순진한(??)
- 데이터 사이에 conditional Independence하다고 가정 하고 예측  

## 1. Optimal Classification 

Optimal predictor of Bayes classifier

- $$f* = argmin_f P(f(X) \neq Y) $$
    - f(X)는 y를 예측 = $$\hat{y} $$ = y의 예측값 
    - $$ \hat{y}$$과 y가 같지 않을 확률(P)을 최소화 해주는 f값을 f*(Optimize func)라고 정의 

        
![](http://i.imgur.com/Cd6zHww.png)
- 유도한 식은 사전 정보를 이용하는 식
- 식비례관계(argmax)이므로 둘이 같은 답을 의미함
- 베이지 이론 활용한것 

###### [문제 풀이]
> 확률 문제 해결 MLE/MAP로 처리 

- Prior = Class Prior = P(Y=y)
- Likelihood = Class COnditional Density = P(X=x|Y=y)

## 2. Conditional Independence 
- 두 변수 사이에는 연관 관계가 없다. 

$$P(x_1|x_2, y) = P(x_1|) $$

eg. P(태풍|비, 천둥) = P(태풍|천둥)

천둥이 친다면 p의 확률로 태풍이 온다. 이때 비에 영향을 받지 않는다. 

## 3. Marginal Independence 

![](http://i.imgur.com/1pHARWx.png)

- Commander가 없을때는 OfficerB의 행동이 OfficerA에 영향을 미침
- Commander가 있을때는 OfficerB의 행동이 OfficerA에 형향을 안 미침 

>  commander는 Y, Officer는 $$X_1, X_2$$로 볼수 있음

## 4. 문제점 
나이브 = conditional	independent	assumption
- Problem	1:	Naïve	assumption
- Problem	2:	Incorrect	Probability	Estimations