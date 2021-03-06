# Machine Learning 개요
- 머신러닝의 그림을 조망하고 주요 영역과 가장 중요한 랜드마크인 지도 학습,  
  비지도 학습, 온라인 학습, 배치 학습, 사례 기반 학습과 모델 기반 학습 파악
- 주요 문제점과 머신러닝 시스템을 평가, 세밀하게 튜닝하는 방법을 다루는 방법

## 머신러닝이란? 
- 머신러닝은 데이터에서부터 학습하도록 컴퓨터를 프로그래밍하는 과학(또는 예술)

## 머신러닝을 사용하는 이유
- 머신러닝 기법에 기반을 둔 스팸 필터는 <b>스팸에 자주 나타나는 패턴을 감지하는 것이</b> 단순 시스템과의 차이점
- 머신러닝 시스템은 변화를 자동으로 감지하여 적응함
  ex) 사용자가 스팸이라고 지정하면, 이를 자동으로 패턴을 감지해 비슷한 메일을 자동으로 스팸으로 인식
- <b>데이터 마이닝 :</b> 머신러닝 기술을 적용해서 대용량의 데이터를 분석하면 겉으로는 보이지 않던 패턴을 발견하는 행위

## 머신러닝이 뛰어난 분야
- 기존 솔루션으로 많은 수동 조정과 규칙이 필요한 문제
  - 하나의 머신러닝 모델이 코드를 간단하게 만들고 전통적인 방법보다 더 잘 수행되도록 할 수 있음
- 전통적인 방식으로는 해결 방법이 없는 복잡한 문제
  - 가장 뛰어난 머신러닝 기법으로 해결 방법을 찾을 수 있음
- 유동적인 환경
  - 머신러닝은 새로운 데이터에 적응할 수 있음
- 복잡한 문제와 대량의 데이터에서 통찰 얻기

## 머신러닝 시스템의 종류
- 사람의 감독하에서 훈련하는 것인지 그렇지 않은 것인지(비지도, 지도, 준지도, 강화)
- 실시간으로 점진적인 학습을 하는지 하지 않는지(온라인 학습, 배치 학습)
- <b>단순하게 알고 있는 데이터 포인트와 새 데이터 포인트를 비교하는 것인지 아니면 과학자들이 하는 것처럼 훈련 데이터셋에서 패턴을 발견하여 예측 모델을 만드는지</b>

### 학습하는 동안의 감독 형태와 정보량에 따른 분류
- 지도 학습
  - KNN, LM, logistic Regression, SVM, DT, RF, NN
- 비지도 학습
  - k-means, DBSCAN, HCA, one-class SVM, isolation Forest
  - PCA, kernel PCA, LLE(locally-linear embedding)
  - t-SNE, Apriori, Eclat
  - 시각화(Visualization) 알고리즘
    - 2D, 3D 시각화 적용: 데이터가 어떻게 조직되어 있는지 이해할 수 있고 예상하지 못한 패턴을 발견할 수 있음
  - 차원 축소 
    - ex) 상관관계가 있는 여러 특성을 하나로 합치는 것 --> 특성 추출
  - 이상치 탐지
    - ex) 부정 거래를 막기 위해 신용카드 거래 감지, 제조 결함 확인 등
  - ex) 블로그 방문자에 대한 계층적 군집 분석
  - 연관 규칙 학습
- 준지도 학습(semi-supervised Learning)
  - 대부분의 데이터가 레이블이 없고 몇 개만 레이블이 있는 경우 학습할 경우 준지도 학습이라고 함
  - ex) 구글 포토 호스팅 서비스
  - 지도 학습과 비지도 학습의 조합으로 이루어져 있음
  - 심층 신뢰 신경망(deep belief network(DBN))은 여러 겹으로 쌓은 제한된 볼츠만 머신(restricted Boltzmann machine(RBM))이라 불리는 비지도 학습에 기초

- 강화 학습(reinforcement Learning)
  - 학습하는 시스템을 에이전트라고 부르며 환경을 관찰하여 행동을 실행하고 그 결과 보상 또는 벌점을 받는 형태
  - 시간이 지나면 최고의 보상을 받기위한 정책(policy)라고 부르는 최상의 전략을 스스로 학습함

### 배치 학습과 온라인 학습
- 온라인 학습
  - 모델 학습에 필요한 데이터를 부분적으로 사용하여 모델을 만들어내는 학습 방법
  - 데이터를 순차적으로 미니배치라고 부르는 작은 묶음 단위 또는 한개씩 학습시킴
  - 온라인 학습이라는 용어에 혼동x, 보통 오프라인에서 학습함
  - <b>외부 메모리(out-of-memory) 학습</b> : 컴퓨터 한 대의 메인 메모리에 들어갈 수 없는 아주 큰 데이터셋을 학습하는 시스템에도 온라인 학습 알고리즘 사용 가능
  - 새로운 데이터 학습시 나쁜 데이터 유입의 경우, 시스템 성능이 점진적으로 나빠질 수 있음
  - 
- 배치 학습  
  - 모델 학습에 필요한 데이터를 한꺼번에 사용해 모델을 만들어내는 학습 방법
  - 모델이 데이터를 기반으로 점진적으로 학습할 수 없음
  - 많은 컴퓨팅 자원이 필요
  
### 사례 기반 학습과 모델 기반 학습 
- 머신러닝 시스템은 어떻게 모델이 일반화 되는가에 따라 달라질 수 있음
- 사례 기반 학습
  - 데이터의 사례를 기억하여 학습하는 형태
  - 유사도 측정을 통해 새로 들어온 데이터를 일반화함
- 모델 기반 학습
  - 데이터를 학습하여 가장 잘 일반화할 수 있는 가중치(파라미터) 값을 정하는 모델 기반 학습
  - 이 모델을 만들어 예측에 사용


## 나쁜 데이터란? 
- 충분하지 않는 양의 데이터
  - 시간과 돈을 알고리즘 개발에 쓰느냐, 아니면 데이터 품질에 적용을 하느냐에 따른 trade-off를 잘 생각해야 함
- 대표성이 없는 데이터  
  - 샘플링 잡음(양이 작은 데이터에서 샘플링), 샘플링 편향(데이터의 양이 큰 곳에서 잘못 샘플링 한 경우) 등을 조심해야 함
- 낮은 품질의 데이터  
  - 많은 data noise, data 결측, 이상치 등..
- 관련 없는 특성
  - feature selection, feature extraction 등을 수행

## 나쁜 모델
- 훈련 데이터 과대적합(overfitting)
  - overfitting을 줄이려면, 데이터 증가시키기  
  - 모델 규제(regularization)
  - 데이터 잡음 줄이기
  - 모델 제약을 가하여 단순화 시키기  
- 훈련 데이터 과소적합(underfitting)
  - 특성 추가
  - 파라미터가 더 많은 모델로 변경
  - 규제 줄이기

## 테스트와 검증
- 테스트 데이터로 오류율을 계산하는 것을 <b>일반화 오차(generalization error), 또는 외부 샘플 오차(out-of-sample error)라고 함</b>
- <b>하이퍼파라미터 튜닝 검증 위하여 테스트 데이터를 여러번 사용하게 되면 테스트 데이터에 과적합될 우려가 있으므로, 하이퍼파라미터 튜닝시 validation set 사용해야 함</b>
- 훈련세트의 일부를 떼어내어 여러 후보 모델을 평가하고 가장 좋은 하나를 선택하는 홀드아웃 검증을 사용
- 가장 좋은 방법은 테스트 세트로 단 한번의 테스트를 수행하는 것
- <b>데이비드 윌퍼트는 데이터에 관해 완벽하게 어떠한 가정도 하지 않으면 특정 모델을 선택할 어떠한 근거도 없다고 말함</b> --> NFL(No Free Launch) 이론이라고 함
- 검증 세트와 테스트 세트에 대표 사진이 배타적으로 포함되어 있어야 하며, 이 사진을 섞어서 반은 검증 세트에 반은 테스트 세트가 실전에서 기대하는 데이터를 가능한 한 잘 대표해야 함
- <b>검증 세트와 테스트 세트에 중복된 데이터가 들어가서는 안됨</b>
- 데이터 불일치를 조심하자 --> 실제 ML 시스템 운영시 예측할 데이터와 validation/test 데이터와 일치하는가? 
