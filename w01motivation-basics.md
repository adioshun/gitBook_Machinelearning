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

###### Step 1. log()를 이용하여 자승을 쉽게 변환 

$$ \hat\theta = argmax_\theta \ln P(D|\theta) = argmax_\theta \ln \{\theta^{aH}(1- \theta)^{aT}\}   = argmax_\theta \{aH \ln \theta + aT \ln(1- \theta)\} $$

> log를 이용하면 값은 달라 지지만, P가 최대가 되는 점과 = log(p)가 최대화 한점은 같음 


## 3. 최대 사후 확률


## 4. 확률과 분포 