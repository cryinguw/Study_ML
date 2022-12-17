유데미에서 다양한 강의들을 공부하며 나만의 것으로 하고자 정리하였다.

[1. 회귀](#회귀)

[2. 분류](#분류-classification)

[3. 군집화](#군집화-clustering)

[4. 연관 규칙 학습](#연관-규칙)

[5. 강화 학습](#강화-학습)

[6. 자연어 처리](#자연어-처리-nlp)

[7. 차원 축소](#차원-축소)
*  *  *
# 회귀
### 1.1 직급 수준에 따른 연봉 예측


csv에 직급에 따라 연봉이 책정 되어있음을 볼 수 있다.


![cap](https://user-images.githubusercontent.com/118944645/206458197-e19a7486-5825-45d2-89d0-2b0cc38532a0.png)


그런데 레벨이 소수점이면 어떻게 책정해야 할까?


다양한 비선형 회귀 방법으로 찾아보고자 한다.


1. 다항식 회귀
2. 소프트 벡터 머신 회귀
3. 의사 결정 트리 회귀
4. 랜덤 포레스트 회귀


### 1.2 시간당 전기 에너지 출력 예측


출처: https://archive.ics.uci.edu/ml/datasets/combined+cycle+power+plant#


위에서 배운 내용은 적은 데이터로 예측하는 것이기 때문에 회귀값이 매우 다르게 나온다.


많은 데이터를 가지고 5가지 회귀에 대한 R2값을 비교하고자 한다.


설명변수 4개(온도(AT), 배기 진공(V)순, 주변 압력(AP), 상대 습도(RH)), 반응변수 1개로 되어있다.


![at](https://user-images.githubusercontent.com/118944645/206851085-8b0d06ba-d9c2-426b-a66c-737496b15184.png)


결론


1. 다중선형회귀: 0.933
2. 다항식 회귀: 0.946
3. SVR: 0.948
4. 의사결정나무: 0.923
5. 랜덤포레스트: 0.962


53214순으로 랜덤포레스트가 가장 높은 R2값으로 선형 상관관계가 좋다고 볼 수 있다.
* * *
# 분류 (Classification)
### 2.1 신제품 출시 후 구입 여부

![qew](https://user-images.githubusercontent.com/118944645/206909375-ee1b5928-d893-4106-8df9-a7756d408006.png)

1. 로지스틱 회귀: 0.89
2. KNN: 0.93
3. SVM: 0.9
4. SVM (Kernel): 0.93
5. 나이브 베이즈: 0.9
6. 의사 결정 나무: 0.91
7. 랜덤포레스트: 0.91

### 2.2 유방암 양성 여부 예측하기


더 많은 범주형 데이터를 가지고 종양이 양성인지 여부에 대해 예측하고자 한다.


K-겹 교차 검증, 그리드 검색과 XGBoost까지 추가하여 공부하였다.


![12](https://user-images.githubusercontent.com/118944645/206906681-de9ef36e-89c1-4e4d-9afc-fda96d83b2c2.png)


설명변수: 종양 두께, 세포 크기 균일성, 세포 모양 균일성, 가장자리 부착, 단독 상피조직 세포, 맨세포핵, 순한 염색질, 정상 핵소체, 세포분열


반응변수: 종양 양성 음성


1. 로지스틱 회귀: 0.947
2. KNN: 0.947
3. SVM: 0.942
4. SVM (Kernel): 0.953
5. 나이브 베이즈: 0.942
6. 의사 결정 나무: 0.959
7. 랜덤포레스트: 0.936
8. K-겹 교차 검증, 그리드 검색: 97.07(+-2.18)%
    - 그리드 검색에서 C가 0.5, 감마가 0.6, kernel이 rbf인 경우가 97.27%로 가장 높은 정확도가 나온것을 볼 수 있다.
9. XGBoost: 97.8%

결론: 기존 7가지 방법으로 했을때 의사결정나무가 95.9%로 가장 높은 정확도를 보여줬으나,

XGBoost의 정확도가 97.8%로 예측이 3개만 틀릴만큼 굉장히 높다.

테스트 세트가 편향될 의향이 있을 수 있으므로, k-겹 교차 검증을 통해 다른 테스트 세트의 정확도를 계산해본 결과 96.53(+-2.07%)로 역시 높은 정확도를 보여준다.
* * *
# 군집화 (Clustering)
### 3.1 쇼핑몰 고객 분석

1. K-평균 클러스터링
2. 계층적 클러스터링

![21](https://user-images.githubusercontent.com/118944645/207060686-d2a85540-c2fc-4abf-b210-17b82c2c2ce8.png)

남녀, 나이, 연간 수입, 소비스코어 순으로 이뤄져 있다. 수입과 소비스코어가 연관성이 있어 보여 2셋을 이용하여 분석을 하였다.

K-평균 클러스터링에서는 Elbow Method로 최적군집수를 정한 후 시각화를 한다.

계층적 클러스터링에서는 dendrogram으로 최적군집수를 정한 후 시각화를 한다.
* * *
# 연관 규칙
### 4.1 지지도를 이용한 상품 추천

고객들이 이전에 구매한 이력을 기반으로 무엇을 구매할지 예측 후 추천하는 방법

![qwe](https://user-images.githubusercontent.com/118944645/207594411-9b2034e8-231f-4896-92e6-7460b1fb1ea4.png)

7500명의 고객들이 구매한 제품들 데이터이다.

이를 통해 최고의 묶음 상품으로 할 수 있는 것을 예측해본다.

apriori: 가장 보편적인 모델

1. 지지도와 신뢰도 설정
2. 빠른 학습을 위해 설정한 최소 지지도보다 높은 지지도를 가진 거래 내역을 가져온다.
3. 높은 신뢰도를 가진 부분집합의 모든 규칙을 가져온다.
4. 감소하는 향상도에 따라 규칙을 분류

eclat

지지도로만 분석하기 때문에 apriori보다 단순하다.

1. 최소 지지도 설정
2. 거래 내역에서 최소 지지도보다 높은 지지도를 가진 모든 부분 집합 가져오기
3. 지지도가 감소하는 순으로 부분 집합 살펴보기
* * *
# 강화 학습
### 5.1 잠재적인 고객으로 만들수 있는 효과적인 광고 선택

새로운 차를 팔려고 하는 자동차 판매점에서

몇 가지 광고의 클릭률을 최적화하여 잠재적인 자동차 구매자를 찾도록 한다.

![qwer](https://user-images.githubusercontent.com/118944645/207606815-a7ff6322-1edf-4130-a2f2-bb00c32b1b4b.png)

클릭 1 아니면 0

UCB와 톰슨 샘플링은 둘 다 멀티 암드 밴딧 문제를 해결한다.

1. UCB

결정론적 알고리즘. 무작위성이 머신에 달려있어서 더 많이 수정 가능

매 라운드 마다 결과 값을 통합하는 업데이트 요구로 인한 많은 비용 발생.

2. 톰슨 샘플링

확률적 알고리즘. 머신에서 이전의 값을 받고난 후 재실행하면 모두 달라진다. 

바로 알 수 없다. 설정한 라운드 뒤에 알 수 있음 

UCB보다 더 잘 작동되기 때문에 보편적으로 사용한다.
* * *
# 자연어 처리 (NLP)

![sad](https://user-images.githubusercontent.com/118944645/207871004-51338095-481d-474d-b274-92f3cb727c15.png)

텍스트를 보고 긍정평가(1)인지 부정평가(0)인지 확인해보고자 한다.

나이브 베이즈 분류기를 통해 데이터 테스트를 해보고 혼동 행렬과 분류성능평가지표를 보고 정확도를 살펴보자.
* * *
# 차원 축소

머신러닝의 한 부분으로 많은 특징들이 들어있는 큰 데이터 세트를 다룰 때는

차원을 축소해서 복잡함을 줄여주는 것이 목적이다.

PCA: unsupervised learning, 존재하는 특징을 기반으로 새로 추출된 특징을 생성하는 것이다. 데이터의 클래스의 차이가 평균보다 분산의 차이에 있을 때, PCA는 LDA보다 뛰어난 성능을 보여준다.

LDA: Supervised Learning, 분류를 할 때 클래스 내의 분산은 최소가 되도록 하되, 클래스끼리의 분산은 최대가 되도록 한다는 것이다. 데이터의 클래스의 차이가 분산보다 평균의 차이에 있을 때, LDA는 PCA보다 뛰어난 성능을 보여준다. 3D plot으로 데이터를 표현할 때, LDA는 PCA보다 뛰어난 성능을 보여준다.

Kernel PCA: Kernel SVM이 SVM보다 좋은 예측력이 보인 것처럼 Kernel PCA도 잘 나오는지 확인해보자.

### 고객 취향에 맞는 와인 예측하기

클러스터링을 통해 고객들의 다양한 분류를 식별

![321](https://user-images.githubusercontent.com/118944645/208232620-f73cf9cf-4790-42eb-95cd-37cc8cd22fe0.png)

3가지 식별에 성공을 했는데

더 적은 양의 특징을 통해 데이터 세트의 복잡성을 감소시키고 싶어한다.

새로운 와인이 들어오면 어떤 고객에게 판촉을 할지 예측하자.
