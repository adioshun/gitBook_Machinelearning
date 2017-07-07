# Week 01 

## 1 동기 

- 지도학습, 비지도 학습

## 2. 최우추정법 (MLE)

동전 던지기 문제 
- Binomial Distribution 
- $$P(D|\theta) = \theta^{aH}(1-\theta)^{at}$$
    - D= 앞면, 뒷면
    - $$\theta$$ = 확률, p 
    - aH = 앞면, aT = 뒷면 

$$\theta$$가 주어진 환경에서 D가 관측될 확률 구하기($$P(D|\theta)$$
- 방법 : 최우 추정법 


### 2.1 정의 
Choose $$\theta$$ that maximizes the probability of observed data 

### 2.2 수식
$$ \hat\theta = argmax_\theta P(D|\theta)   $$

### 2.3 문제 풀이 
###### Step 1. 식 변환 
$$ \hat\theta = argmax_\theta P(D|\theta) = argmax_\theta\theta^{aH}(1- \theta)^{aT}   $$

###### Step 2. log()를 이용하여 자승을 쉽게 변환 

$$ \hat\theta = argmax_\theta \ln P(D|\theta) = argmax_\theta \ln \{\theta^{aH}(1- \theta)^{aT}\}   = argmax_\theta \{aH \ln \theta + aT \ln(1- \theta)\} $$

> log를 이용하면 값은 달라 지지만, P가 최대가 되는 점과 = log(p)가 최대화 한점은 같음 

###### Step 3. Maximization problem으로 변했으므로 이를 해결
- 즉, 식에 있는 변수 중에서 $$\theta$$을 최적하여 수식 전체값을 최대(argmax)화 하는 문제
- 최대화 = 미분하여  0 되게 

$$ \frac{d}{d \theta}(aH \ln \theta + aT \ln(1- \theta) = 0 $$

$$\rightarrow \frac{aH}{\theta} - \frac{aT}{1-\theta}=0$$

$$ \rightarrow \theta = \frac{aH}{aT+aH} $$

즉, $$\frac{관측값}{전체값}$$


### 2.4 에러율 정의 (PAC)
PAC (Probably Approximately Correct) learning
- 이론적으로 모델의 성능을 측정하는 방법 중 하나
- “높은 확률로 (Probably)” 주어진 모델이 “작은 error를 가진다 (Approximatly Correct)”

호에프딩의 부등식(Hoeffding's inequality)으로 에러 바운더리를 표현 하기 
$$P(|\hat{\theta} - \theta^*|\geq \epsilon)\leq 2e^{-2N\epsilon^2}$$
    - $$\theta^*$$= 실제값, $$\epsilon$$=에러바운드 

> 에러바운드(식 우측$$\epsilon$$)가 커지면 확률(식 좌측)은 작아짐

> 시행횟수(식 우측n)가 커지면 확률(식 좌측)은 작아짐 

## 3. 최대 사후 확률 (MAP[^1])

### 3.1 정의 
사전정보(추정정보,Prior Knowledge)를 이용하여 $$\theta$$구하기 by Bayes

### 3.2 수식 
$$ posterior = \frac{MLE \times Prior Knowledge}{Normalizing Constant}= P(\theta|D)=\frac{P(D|\theta)P(\theta)}{P(D)} $$

> P(D)는 이미 정해진것이고, 중요한 영향을 안 줌, 빼고 계산

> 값을 뻇으므로 = 이 아닌 비례기호($$ \propto $$) 사용


### 3.3 문제 풀이 

###### Step 1. 상수빼고 비례기호로 식 재 정의 

$$ P(\theta |D) \propto P(D|\theta )P(\theta) $$
  

###### Step 2. 분포에서 값 가져 오기(??) 
- $$P(D|\theta) = \theta^{aH}(1-\theta)^{aT} $$ = 이항분포에서 가져 오기 

- $$P(\theta)$$ = 사전지식 = Beta 분포($$P(\theta)=\frac{\theta^{\alpha-1}(1-\theta)^{\beta-1}}{B(\alpha,\beta)}$$)에서 가져 오기


> 왜 사전지식을 Beta 분포에서 가져 오나? 어느 분포에서 가져 와도 상관 없으나, Beta분포가 예시에는 적절함

###### Step 3. 식 재 정리 

|위식 $$P(\theta)=\frac{\theta^{\alpha-1}(1-\theta)^{\beta-1}}{B(\alpha,\beta)}$$에서 $$B(\alpha,\beta)$$는 $$\theta$$와 관계 없으므로 제거 하여 아래 식 생성, 제거 하였으므로 $$\propto$$표시 |
|-|

$$ P(\theta |D) \propto \theta^{aH}(1-\theta)^{aT} \cdot \theta^{\alpha-1}(1-\theta)^{\beta-1} $$
$$ P(\theta |D) \propto \theta^{aH+\alpha-1}(1-\theta)^{aT + \beta-1}$$ 


$$ \hat{\theta} = \frac{aH+\alpha-1}{(aH+\alpha-1)+(aT + \beta-1)}$$

> MLE에 비해 MAP에 $$\alpha, \beta$$가 식에 추가적으로 존재 

> 시도횟수가 많으면 점점 사라짐. 하지만, 시도횟수가 적으면 사전 정보는 사라지지 않고 중요한 역할 차지 

> 즉, 시도가 적으면 MLE $$\neq$$ MAP이고, 많으면 MLE = MAP



## 4. 확률과 분포 

### 4.1 확률
MLE/MAP를 통해서 알아본값 


### 4.2 확률 분포
- A func. mapping an event to a probability 

#### A. Normal Distribution 

#### B. Beta Distribution 
- 범위가 정해져 있는 경우 : eg. 확률 

#### C. Binomial Distribution 
- O or 1 등 두개의 값이 나올경우 : eg. 동전 던지기 
- Discrete 상





## 5. 베이즈 정리 
18세기 영국의 수학자 토마스 베이즈(Thomas Bayes)가 도입.

사후 확률 문제를 사전확률을 활용하는 문제로 바꾸어 줌 


### 5.1 용어 

![](http://i.imgur.com/0S88upq.png)
- 주머니 : 10장의 종이 (7장 A라고 쓰임, 3장 B라고 쓰임)
- 상자 A : 10개의 공 (8개 파란공, 2개 하얀공)
- 상자 B : 15개의 공 (6개 파란공, 9개 하얀공) 


확률 : 주머니에서 종이를 꺼낼때 A가 나올 확률 P(A)=7/10 

조건부 확률 : 상자 A에서 공을 꺼낼때 하얀공이 나올 확률 P(하얀|A) = 2/10

결합 확률 :주머니에서 A나오고, 상자 A에서 하얀공 나올 확률 P(A, 하얀) = P(하얀|A)P(A) = (2/10)(7/10) = 7/50

주변 확률 : 하얀공이 나올 확률 = A가 선택되고 하얀공 + B가 선택되고 하얀공 = P(하얀|A)P(A) + P(하얀|B)P(B) = (2/10)(7/10) + (9/15)(3/10) = 8/25

[문제] 하얀 공이 나왔는데 A에서 나왔는지 B에서 나왔는지 맞추는 문제. 

- 사전확률(Prior Probability)  : 추가적 정보가 주워지기전의 정보, Event가 연속적으로 일어 날때 전에 이미 경정된 확률, P(A), P(B)
- 사후확률(Posterior Probability) : 추가적 정보가 주워진 상태에서의 사전확률, 조건부확률과 같음 P(A|하얀), P(B|하얀)



4. 사전확륙과 사후확률을 알고 있다면 우도확률(Likehood Probability)을 구할 수 있다.

http://blog.daum.net/crexy/11051499



---




---
[^1]: maximum a posteriori, MAP
