# Support Vector Machine (SVM)

![](http://i.imgur.com/QEoOAb9.png)

- Vladimir Vapnik이 제안

- 기존 분류기 : 기존 방법들은 오류율을 최소화
- SVM 분류기 : 부류 사이에 존재하는 margin(여백)을 최대화 하여 일반화 능력을 극대화

- 분류 오차를 줄이면서 동시에 여백을 최대로 하는 결정 경계(decision boundary)를 찾음
    - 여백 = 일반화 성능 강화 

- 이진 분류기(binary classifier)이나 M 분류로 확장 가능 

![](http://i.imgur.com/uF7mAZO.png)
[H2, H3 모두 분류 조건을 만족하나, H3가 더 일반성 높음]

- 여백(margin): 결정 경계와 가장 가까이에 있는 학습 데이터까지의 **거리**

- 서포트 벡터(support vector): 결정 경계로부터 가장 가까이에 있는 학습 데이터들, 결정 경계를 결정하게 되는 요소들


