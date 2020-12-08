## xgboost 완전 정복
### 기본 원리
* 일반화 선형 회귀 모델이라고 하며, 종속 변수에 적절한 함수를 적용하는 회귀 모델링 기법
*  종속변수에 적용하는 함수를 link function이라고 부름
* 오차항의 확률 분포가 무엇이냐에 따라 일반적으로 사용하는 link function이 정해져 있음

### 파라미터
* 파라미터를 제대로 이해하고 있어야 시행 착오가 적음
* 이진 분류 문제에 linear-regression을 적용해 놓고 L1, L2 파라미터를 조정하고 있다면 안됨!
* 파라미터 순위 팁
  * eta -> lambda -> alpha  ....

#### R - XGBTree package 파라미터 종류
* gamma : 이 값이 커지면 트리 깊이가 줄어들어 보수적인 모델이 됨
* max depth : maximum depth
* min child weight : 특정 순도에 도달하면 가지치기를 종료.
* eta : learning rate, boosting step 마다 weight를 주어 부스팅 과정에서 과적합이 일어나지 않도록 함
* subsample : 각 트리마다의 train data sampling 비율, 너무 적게 주면 under_fitting 발생
* colsample_bytree : 각 트리마다의 feature 샘플링 비율
