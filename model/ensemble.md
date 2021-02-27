# 앙상블(ensemle)
- 배깅, 부스팅, 스태킹 등 인기있는 앙상블 방법을 설명해 보겠음

## 투표 기반 분류기
- 다수결 투표로 정해지는 분류기를 hard voting 분류기라고 함
- 분류기가 약한 학습기(weak learner) 일지라도 충분하게 많고 다양하다면 앙상블은 강한 학습기(strong learner)가 될 수 있음  
  이 것이 어떻게 가능할까? --> 큰 수의 법칙(law of large numbers)로 설명 가능
- 즉, 51%의 정확도를 가진 1000개의 분류기로 앙상블 모델을 구축한다고 가정했을 때,   
  가장 많은 클래스를 예측으로 삼는다면 75%의 정확도를 기대할 수 있음
- 하지만 이러한 가정은 모든 분류기가 완벽하게 독립적이고 오차에 상관관계가 없어야 가능
- but 앙상블 모형은 같은 데이터로 훈련시키기 때문에 이런 가정이 맞지 않음
- 앙상블 방법은 예측기가 가능한 한 서로 독립적일 때 최고의 성능을 발휘함. 즉 다양한 분류기를 얻는 한 가지 방법은  
  각기 다른 알고리즘으로 학습시키는 것. 이렇게 하면 매우 다른 종류의 오차를 만들 가능성이 높기 때문에 앙상블 모델의 정확도를 향상시킴
- 모든 분류기가 클래스의 확률을 예측할 수 있으면(`predict_proba()` 메서드가 있으면) 개별 분류기의 예측을 평균 내어 확률이 가장 높은 클래스를 예측할 수 있음  
  이를 soft voting라고 함

## bagging, pasting
- 훈련 세트를 중복을 허용하여 샘플링하는 방식을 bagging, 중복 허용을 안하는 방식을 pasting 이라고 함
- 개별 예측기는 원본 훈련 세트로 훈련시킨 것보다 훨씬 크게 편향되어 있지만 수집 함수를 통과하면 편향과 분산 모두 감소
- 일반적으로 앙상블의 결과는 원본 데이터셋으로 하나의 예측기를 훈련시킬때와 비교해 편향은 비슷하지만 분산은 줄어듬  
  즉, <b>훈련 세트의 오차 수는 거의 비슷하지만, 결정 경계는 덜 불규칙하다는 의미</b>
- 해당 모델을 다른 CPU 코어나 서버에서 병렬로 훈련시킬 수 있어 인기가 많음
- `BaggingClassifier` 클래스는 기반이 되는 분류기가 결정 트리 분류기처럼 클래스 확률을 추정할 수 있으면 hard voting 대신 soft voting 수행
- <b>부트스트래핑은 각 예측기가 학습하는 서브셋에 다양성을 증가시키므로, 배깅이 페이스팅보다 편향이 좀 더 높고, 분산이 적어 더 선호됨</b>
- 시간과 여유가 있다면 교차 검증으로 둘 다 비교하는 것이 좋음

### oob 평가
- 배깅을 사용하면 어떤 샘플은 선택되고, 어떤 샘플은 선택되지 않을 수 있음
- `BaggingClassifier`는 기본값으로 중복을 허용하여 훈련 세트 m개의 샘플을 선택하는데, 이는 평균적으로  
  훈련 샘플의 63.2% 정도만 샘플링된다는 것을 의미함
- 선택되지 않은 나머지 37%를 oob(out-of-bag) 샘플이라고 부름
- 앙상블의 평가는 각 예측기의 oob 평가를 평균하여 얻음

![img](bagging_ensemble.JPG)

## 용어 정리
- 큰 수의 법칙(law of large numbers)
  - 동전을 자꾸 던질수록 실제 확률에 점점 더 가까워 지는 것을 말함  
    예를 들어 앞면이 51%, 뒷면이 49%가 나오는 동전이 있다고 할때 동전을 점점 더 여러번 던질수록  
    해당 확률에 가까워짐을 의미함
  - 동전을 1000번 던진 후 앞면이 다수가 될 확률은 75%, 10,000번 던지면 확률이 97%까지 높아짐