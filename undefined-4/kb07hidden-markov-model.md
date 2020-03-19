# KB07\_Hidden\_Markov\_Model

## 1. 개념

* 은닉 :
* 마코브 : 마코브 체인 이론\(시간 r에서의관측은 가장 최근 r개의 관측에만 의존 한다\)
  * 0차 마코브 체인 : 과거를 보지 않음, 과거에 독립적
  * 1차 마코브 체인 : 바로 이전의 관측데이터만 활용
  * 2차 마코브 체인 : 바로 이전 두 개의 관측을 본다. 
* 모델 : 확률 모델

![](http://i.imgur.com/1qseFFs.png)

## 1. 마코브 모델

### 1.1 개요

* 이미 주어진 환경에서 관측 데이터의 발생 확률
  * eg. 오늘 해가 떳는데 내일부터 7일간의 날씨가 해-해-비-비-해-구름-해일 확률은
  * eg. 손글씨에서 체인코드 1-0-7-6-5-5-7-0-0으로 표현되는 샘플이 발생 할 확률은 
* 1차 마코프 체인 사용
  * 2차 이상에서는 추정할 매개 변수가 많아 현실적인 문제 발생
* 알파벳을 구성하는 기호 각각을 상태로 간주
* 예: 날씨
  * V={비, 구름, 해}
  * 기후 관측에 의해 얻은 날씨 변화 확률

![](http://i.imgur.com/tAb4men.png)

### 1.2 마코브 모델 표현법

* 상태 전이 확률 행렬
* 상태 전이도 

![](http://i.imgur.com/4nH8foU.png)

### 1.3 마코브 모델 활용: 관측벡터 O의 확률 구하기

![](http://i.imgur.com/3eNoqCf.png) L3에서 L4로 넘어 가는 단계는 결합확률을 조건부 확률로 변경 \(체인규칙 이용\)

### 1.4 \[예제\] 1차, 0차, 2차 마코브 체인 만들기

![](http://i.imgur.com/kOgUvh8.png)

#### A. 1차 마코브 체인

**Step 1. 마코브 모델 생성**

상태 전이 확률 행렬 A

![](http://i.imgur.com/to6Krip.png)

> 현재 관측\(t-1\)이 7일때 다음 관측\(t\)이 0일 경우 = 4 \(첫 샘플 2번, 두번째 샘플 1번, 세번쨰 샘플 1번\)

초기 확률, $$\pi_i = P(o_1 = v_1)$$

![](http://i.imgur.com/1NLYbPu.png)

> 세 개 샘플의 t=1일떄의관측값 = 1,0,4 \(??? 어떻게 값이 나온거지??\)

**Step 2. 샘플 발생 확률 계산**

![](http://i.imgur.com/10hxRkj.png)

#### B. 0차 마코프 체인 만들기

**Step 1. 마코브 모델 생성**

상태 전이 확률 행렬 A

![](http://i.imgur.com/LWfg1UJ.png)

**Step 2. 샘플 발생 확률 계산**

손글씨에서 체인코드 1-0-7-6-5-5-7-0-0으로 표현되는 샘플이 발생 할 확률은

![](http://i.imgur.com/0kE7jOp.png)

#### C. 2차 마코프 체인 만들기

**Step 1. 마코브 모델 생성**

상태 전이 확률 행렬 A

![](http://i.imgur.com/39BZqZD.png)

> 최근 2개의 값을 관측하기 위해 64\*8 행렬 필요

**Step 2. 샘플 발생 확률 계산**

손글씨에서 체인코드 1-0-7-6-5-5-7-0-0으로 표현되는 샘플이 발생 할 확률은

### 1.5 마코브 모델의 제약

모델링 능력에 한계 있음 = 복잡한 실 세계 현상을 제대로 모델링 못함

## 2. 히든 마코브 모델

### 2.1 개요

* 마코브 모델의 제약 : 모델의 크기\(=추정해야 하는 매개 변수의 개수\)가 상태의 개수\(m\), 고려해야할 과거 시점\(r, 0차~3차 마코브체인\)에 따라서 $$m^r(m-1)$$만큼 증가한다.
* 해결 방안\(HMM\) : 차수\(r\)을 미리 고정하지 않고 모델 자체가 확률 프로세스에 따라 적응 하도록 정함
  * `상태를 감춤`으로서 가능 
  * 아무리 먼 과거의 관측도 현재에 영향을 미침

![](http://i.imgur.com/GC9Ztmy.png) **\[ "상태"를 감추었다는 것이 둘의 큰 차이점\]**

#### A. 마코프 모델\(예, 해-해-비-구름이 관측\)

상태 s3-s3-s1-s2에서 관측한 것이다.

#### B. 은닉 마코프 모델\(예, 해-해-비-구름이 관측\)

모든 상태에서 {비,해,구름}이 관측 가능하므로 3 x 3 x 3 x 3 =81 가지 경우가 있음

* 상태 s3-s3-s1-s2일 수도 있고 
* 상태 s1-s2-s3-s1일 수도 있다. 
* .....

예를 들어 상태 s3-s3-s1-s2에서 관측될 확률 : $$[\pi_3 * b_3(해)]*[a_{33}*b_3(해)]*[a_{31}*b_1(비)]*[a_{12}*b_2(구름)]$$

**\[예제\] 여자 친구의 삶**

날씨\(상태:해,비\)에 따른 여자 친구의 일상을 관찰, V={산책, 쇼핑, 청소}

![](http://i.imgur.com/JpuOmxx.png)

**Step 1. 히든 마코브 모델 생성**

![](http://i.imgur.com/FloGU7R.png)

> 날씨는 감추어져 있다. 날씨에 대해서는 말하지 않고 그녀가 한 행동만 알수 있다.

**Step 2. 샘플 발생 확률 계산**

* 그녀가 일주일 연속으로 쇼핑만 할 확률은?
* 그끄저께 산책, 그저께 산책, 어제 청소했다는데 3일간 그곳 날씨는?
* 그끄저께 산책, 그저께 산책, 어제 청소했다는데 오늘과 내일 무얼할까?

### 2.2 구성 요소와 3가지 문제

위 예제는 HMM을 만드는데 필요한 핵심 정보를 알고 있다고 가정하고 있다. \(eg. 날씨는 비or해\)

* 모델을 알때 확률 추론하라.
* 날씨와 그녀의 행위에 대한 확률 분포 알고 있음

이런 정보들도 모르고, 수집된 데이터를 가지고 HMM을 생성하도록 해보자

* 어느 것이 상태인가? 상태는 몇 가지인가? \(아키텍처 설계\)
* 확률 분포는 어떻게 구하나? \(학습\)

#### A. 아키텍쳐 설계

![](http://i.imgur.com/e2TP1Tj.png) 응용의 특성에 따라 적절한 아키텍처 선택 중요

* 어고딕 모델
* 좌우 모델: 음성인식 

#### B. 학습 : 매개변수\($$\Theta = (A,B,\pi$$\) 추정

**가. 상태 전이 확률** 

A는 HMM이 작동하는 도중 다음 상태를 결정하는 데 쓰인다.

행렬 A는 상태 $$s_i$$에서 $$s_j$$로 전이할 확률

![](http://i.imgur.com/rxzAfTY.png)

* $$a_ij$$는 시간 $$t$$에 상태 $$s_i$$에 있다가 $$t+1$$에 $$s_j$$로 이동할 확률 

**나. 관측 확률** 

B는 HMM이 어느 상태에 도달하였을 때 그 상태에서 관측될 기호를 결정 하는데 쓰인다.

행렬 B는 상태 $$s_i$$에서 기호 $$v_k$$를 관측할 확률

![](http://i.imgur.com/G9enVeb.png)

* $$b_j(v_k)$$는 상태 $$s_j$$에서 기호 $$v_k$$가 관측될 확률이다. \(m = 기호의 개수\)

**다. 초기 확률 벡터** 

$$\pi$$는 HMM을 기동시킬 때 어느 상태에서 시작할 지를 결정하는데 쓰인다.

![](http://i.imgur.com/Q5dlDLX.png)

* $$\pi_i$$는 상태 $$s_i$$에서 시작할 확률이다. 

#### C. 3가지 문제

![](http://i.imgur.com/HHCYZZ8.png)

**가. 평가**

모델 $$\Theta$$가 주어진 상황에서, 관측벡터 $$O$$를 얻었을때 $$P(O\mid \Theta)$$는?

* 예\) 필기 인식 문제에서 각 숫자별 인식 모델\($$\Theta_1,\Theta_2,...,\Theta_9$$\)을 만들었을때 사용자 입력\(관측벡터$$O$$\)가 입력되면 각 $$P(O\mid \Theta_1),P(O\mid \Theta_2),...,P(O\mid \Theta_9)$$을 계산하고 가장 높은 것을 분류로 분류 한면 된다.
* 예\) 그녀가 오늘 산책, 내일 산택, 모레 청소, 글피 쇼핑할 확률은 얼마인가? $$P(O_1 =산책,O_2 =산책, O_3 =청소, O_4 = 쇼핑 \mid \Theta )는 얼마인가?$$

**나. 디코딩**

모델 $$\Theta$$가 주어진 상황에서, 관측벡터 $$O$$를 얻었을때 최적의 상태열$$Q=(q_1,q_2,...,q_T)$$은?

여러 후보 상태 열 중에 가장 확률이 높은 것을 찾는 `최적화`문제

* 예\) 그녀가 나흘간 산책, 산책, 청소, 쇼핑하였는데 그 나흘의 날씨를 추정해 보면?

**다. 학습**

훈련집합 $$X={O_1,..,O_N}$$이 주어져 있을때 HMM의 매개 변수 $$\Theta$$는?

X로 HMM을 학습시키는 `최적화`문제

### 2.3 3가지 문제와 알고리즘

> 상세 내용은 교재 참고 패턴인식, 오일석

#### A. 평가

#### B. 디코딩

* Viterbi 알고리즘 

#### C. 학습

평가와 디코딩의 반대 작업

평가와 디코딩 같은 분석적 방법 없음\(수치적 방법 필요\)

관측 벡터 $$O$$의 확률을 최대로 하는 $$\Theta(A,B,\pi)$$를 찾는 문제이다.

**Baum-Welch 알고리즘**

O로 직접 Θ를 찾을 수 없다.

* 은닉 변수latent variable $$\gamma, \kappa$$등장
* 가우시언 혼합 추정과 유사성 있음

![](http://i.imgur.com/KSpkcWl.png)
