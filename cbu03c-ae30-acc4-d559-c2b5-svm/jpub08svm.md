# 서포트벡터 머신

장점 : 적당한 데이터 사이즈도 활용 가능 

단점 : 아주큰 데이터에는 트레이닝에 요구되는 계산 비용이 스케일되지 않으므로 잘 동작하지 않는다. 

수식 

$$y=W \cdot X + b $$
   
- $$W \cdot X =내적 = \sum_i w_ix_i = W^TX$$ 로도 표현 
    
   - 가중치 W는 분류 선에 수직 = $$X^+와 X^-$$를 지나는 거리는 W와 같다. 

- W를 단위 벡터 $$\frac{W}{\parallel W \parallel}$$로 정의 해서 마진(M)이 $$\frac{1}{\parallel W \parallel}$$가 된다. 

- 마진값 M을 최대한 크게 하는것은 $$W^TW$$를 가능한 작게 하는것과 같은 문제 

|최종 목표|
|-|
|$$Min \frac{1}{2}W^TW$$ subject to $$t_i(W^TX_i + b) \geq 1 $$


---

참고 : [SVM Tutorial](https://www.svm-tutorial.com/)