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

P(\theta |D) \propto P(D|\theta )P(\theta) 









## 4. 확률과 분포 



---
[^1]: maximum a posteriori, MAP
