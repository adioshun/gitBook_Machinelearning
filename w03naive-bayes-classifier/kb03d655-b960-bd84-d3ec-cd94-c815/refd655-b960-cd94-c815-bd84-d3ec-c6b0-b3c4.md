# 확률 모형의 모수 추정
모수를 아예 모른다고 가정하고 모집단으로부터 추출된 표본으로부터 모수를 추정하는 방법이다.

![](http://i.imgur.com/D5eLnLK.png)

이처럼 표본을 통해 모집단의 모수를 추정하는 방법에는 크게 세가지가 있다.

1. [method of moments](http://blog.daum.net/gongdjn/51)
2. [method of maximum likelihood](http://blog.daum.net/gongdjn/122)
3. Bayes' method

## 1. method of moments

> 나중에 

## 2. method of maximum likelihood 

만약 추출된 표본으로부터 likelihood function을 구했다면,
likelihood function을 최대로 만들어주는 모수를 찾는 것

|$$L(\hat\theta; x_1,...,x_n) = \max_{\theta \in \Xi}L(\theta; x_1,...,x_n)$$|
|-|
|- $$\Xi$$는 가능한 모든 모수의 집합, $$\theta$$는 모수 |

주어진 샘플  x 에 대해 우도를 가장 크게 해 주는 모수  θ 를 찾는 방법

##### 예제 
정규 분포에서 분산($$\sigma^2 = 1$$), 샘플($$x_1 =1 $$)은 알고 있으나 평균($$\mu$$)을 모를 경우, 
- 어떤 $$\mu(\mu =-1, \mu =0, \mu=1)$$ 값이 가장 가능성(우도)이 있어 보이는가?
- 이 세가지 $$\mu$$값에 대해$$x_0$$이 나올 확률이 바로 우도 이다. 

![](http://i.imgur.com/DC9Eadn.png)

1일 경우의 우도가 가장 크다. 따라서 MLE에 위한 추정값은 1이다. 

> 구현시는 우도를 로그변환한 로그 우도(Log likelihood)함수로 변환 하여 계산 용이 하도록 함(곱셈->덧셈)

###### [참고] MLEs를 이용하여 모수 population parameter 를 추정하는 방법
- [Geometric distribution의 모수 추정하기](http://m.blog.daum.net/gongdjn/123)
- [Poisson distribution의 모수 추정하기](http://m.blog.daum.net/gongdjn/124)
- [Uniform distribution의 모수 추정하기](http://m.blog.daum.net/gongdjn/125)
- [Normal distribution의 모수 추정하기](http://m.blog.daum.net/gongdjn/126)
- Gamma distribution의 모수 추정하기


## 최대 우도법 

선형회귀분석에서는 최소제곱법을 통해 회귀식을 추정하였다. 그러면 종속변수와 독립변수가 선형 관계에 놓여 있지 않는 일반화 선형모형에서는 어떤 방식으로 회귀식을 추정할 수 있을까? 일반화 선형모형에서는 대개 최대우도법(maximum likelihood method)을 이용하여 회귀식을 추정한다



-- 
출처: http://dermabae.tistory.com/188 [높이 비상하는 즐거운 상상]


---

## ref 1. likelihood 

### 1.1 개요 

###### Step 1. 확률 분포 함수는 어떤 모수(파라미터)를 전제로 하고 있다. 
- 확률변수 X에 대한 확률 모형은 확률 밀도 함수 $$F_X$$에 의해 정의 된다. 
- 확률 밀도 함수 : $$F_X(x;\theta)$$
    - $$x$$ : 확률 변수가 가질 수 있는 실수 값
    - $$\theta$$ : 확률 밀도 함수, 확률 모형의 모수(parameter) 집합 eg. 정규 분포 : $$\theta = (\mu, \sigma^2)$$

정규분포 예 

$$

f_X(x;\theta) =  \frac{1}{\sqrt{2\pi\sigma}}e^{-x-\mu^2/2\sigma^2}

$$ 



###### Step 2. 파라미터를 변수로 생각 한다면 아래와 같은 조건부 확률로 표현 할수 있다. 
- $$f(x \mid \mu,\sigma) = f(x ; \mu,\sigma) = \frac{1}{\sqrt{2\pi\sigma}}e^{-x-\mu^2/2\sigma^2} $$
- $$\mu,\sigma$$가 주어 졌을때 x에 대한 확률(밀도) 함수 

함수 입장에서 $$\theta(\mu,\sigma)$$는 상수로 고정된 값이고 $$x$$를 변수로 가정한다. 
- 즉, 이미 확률 변수 모형은 고정되어 있고 주어진 실수 입력값에 대해 그 실수값이 나올 상대적 가능성을 출력

###### Step 3. 역으로 어떤 표본값(x=1)이 주어 졌을때 모수 population parameter 에 대한 함수로 표현하면 어떻게 되나

추정 문제에서는 x는 샘플로 알고 있고, 모수$$(\theta)$$를 모르고 있다 $$L(\theta;x)$$

- $$f(\mu,\sigma) = f(\mu,\sigma) = \frac{1}{\sqrt{2\pi\sigma}}e^{-1-\mu^2/2\sigma^2} $$
- 이와 같은 식을 likelihood function(우도 함수)라고 한다. 



###### Step 4. 최종식/정리 

1. 모수 parameter 가 $$\theta$$로 주어지는 모집단이 존재 한다. 

2. 모집단에서 n개 표본을 추출 하여 각각 확률 변수로 정의 했다. ($$X_1, X_2, ..., X_n$$)

3. 각각의 확률 변수에 특정한 값이 할당 되었다고 가정 ($$X_1=x_1, X_2=x_2, ..., X_n=x_n$$)

4. 한편 $$x_1, x_2, ..., x_n$$의 값이 추출될 확률을 표현하는 결합 확률 밀도 함수가 존재 한다면 이렇게 표현 할수 있다. $$f(x_1, x_2, ..., x_n;\theta)$$
    - 이를 우도 함수라고도 한다. $$L(\theta) =f(x_1, x_2, ..., x_n;\theta) $$

5. 결합 확률 밀도 함수는 개별적인 확률 밀도 함수의 곱으로 나타낼 수 있다.

![](http://i.imgur.com/NbT9lH9.png)


![](http://i.imgur.com/tuwUN5z.png)
> [likelihood가 확률 probability와 개념이 어떻게 다를까.]
probability is appropriate to a situation where observation are going to be made and we are interested in the probabilties of various possible sets of values that might be observed, taking the parameter θ as fixed (even if unknown);
likelihood is appropriate to a situation where data have already been obtained, and all conceivable values of θ are to be considered in the light of the data.


###### [예제]
![](http://i.imgur.com/tyG2W9w.png)





### 1.2 likelihood 


Likelihood =우도,2 尤度, 가능성/가능도

![](http://i.imgur.com/zq4MV1Y.png)

- 모수로부터 특정 현상이 관찰되는 것을 확률의 문제라고 한다면, 우도는 확률의 반대 개념이다. 
    - 주어진 현상을 가지고 이 현상이 추출될 가능성을 가장 높게 하는(우도가 가장 높은) 모수를 거꾸로 추적하는 방법이 최대우도법이다.

- 확률 분포의 모수가, 어떤 확률변수의 표집값과 일관되는 정도를 나타내는 값이다.
    - 구체적으로, 주어진 표집값에 대한 모수의 가능도는 이 모수를 따르는 분포가 주어진 관측값에 대하여 부여하는 확률
    
- 알려진 결과(관측된 표본)에 기초하여 미지의 모수(매개변수)의 추정에 대한 평가 척도
    - 우도 likelihood는 한 개 혹은 몇 개 데이타를 관측해서 그 값들이 어떤 확률분포를 갖는 모집단에서 나왔다고 보는 것이 좋겠는가 하는 유사성이다.
    
- 확률분포함수의 y값, 일어날 가능성이 높은 사건   
    - 주사위 문제: 가능도 = 확률
    - 연속사건(정규분포): 가능동 = PDF


### 1.2 수식

- 확률적으로 조건부확률로 표현할 수 있음 $$p(X\mid \omega_i)$$

### 1.3 활용

- 필요 이유 : 연속사건에서는 특정 사건이 일어날 확률이 전부 0으로 계산되기 때문에 사건들이 일어날 가능성을 비교하는 것이 불가능하며, 가능도라는 개념을 적용해야 이를 비교할 수 있다.

- 나타난 결과에 따라 여러 가능한 가설들을 평가할 수 있는 측도(Measure)임





> 출처 : [정보통신기술용어해설](http://www.ktword.co.kr/abbr_view.php?m_temp1=3214)




