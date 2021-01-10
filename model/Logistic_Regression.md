# 로지스틱 회귀
- 어떤 회귀 알고리즘은 분류에도 사용이 가능
- 로지스틱 회귀는 샘플이 특정 클래스에 속할 확률을 추정하는데 널리 사용됨
- 추정 확률이 50%가 넘으면 모델은 그 샘플이 해당 클래스에 속한다고 예측(레이블이 '1'인 양성 클래스)
- 아니면 클래스에 속하지 않는다고 예측(레이블이 '0'인 음성 클래스)
- 이를 <b>이진 분류기라고 함</b>

## 로지스틱 확률 추정
- 로지스틱도 선형 회귀와 마찬가지로 입력 특성의 가중치의 합을 계산함(그리고 편향을 더함)
- 대신 선형 회귀처럼 결과를 바로 출력하지 않고, 결괏값의 로지스틱을 출력
- 로지스틱 회귀 모델의 확률 추정 모형은 다음과 같음
<p align = 'center'><img src="https://latex.codecogs.com/gif.latex?\hat{p}&space;=&space;h_{\theta}(x)&space;=&space;\sigma(\theta^{T}&space;x)" /></p>

- 로지스틱(sigma(.)로 표현)은 0과 1사이를 출력하는 시그모이드 함수임
- 로지스틱 함수는 다음과 같음
<p align = 'center'><img src="https://latex.codecogs.com/gif.latex?\sigma(t)&space;=&space;\frac{1}{1&space;&plus;&space;exp(-t)}" /></p>
- 로지스틱 회귀 모델이 샘플 x가 양성 클래스에 속할 확률 hatP = h_(theta)(x) 를 추정하면 이에 대한 예측 hatY를 쉽게 구할 수 있음
- 로지스틱 회귀 모델 예측은 다음과 같음
<p align = 'center'><img src="https://latex.codecogs.com/gif.latex?\hat{y}&space;=&space;\begin{pmatrix}&space;0&space;,&space;\hat{p}&space;<&space;0.5\\&space;1,&space;\hat{p}&space;>=&space;0.5&space;\end{pmatrix}" /></p>

- t < 0이면 sigma(t) < 0.5 이고, t >= 0 이면 sigma(t) >= 0.5 이므로, 로지스틱 회귀 모델은 theta^(t) * x가 양수일 때 1이라고 예측하고, 음수일 때 0이라고 예측
- t를 종종 <b>로짓(logit)</b> 이라고 부름. logit(p) = log(p / 1 - p) 로 정의 되는 로짓 함수가 로지스틱 함수의 역함수라는 사실에서 이름을 따옴
- 실제로 추정 확률 p의 로짓을 계산하면 t값을 얻을 수 있음
- 로짓을 <b>로그-오즈(log-odds)</b>라고도 부름. 로그-오즈는 양성 클래스 추정 확률과 음성 클래스 추정 확률 사이의 로그 비율이기 때문

## 훈련과 비용 함수
- 그렇다면 해당 모형을 어떻게 훈련시킬까?
- 훈련의 목적은 양성 샘플(y = 1)에 대해서는 높은 확률을 추정하고, 음성 샘플(y = 0)에 대해서는 낮을 확률을 추정하는 모델의 파라미터 벡터 theta를 찾는 것
- 이러한 아이디어가 하나의 훈련 샘플 x에 대해 나타낸 비용 함수인 다음 식에 드러나 있음
<p align = 'center'><img src="https://latex.codecogs.com/gif.latex?c(\theta)&space;=&space;\begin{pmatrix}&space;-log(\hat{p})),&space;y&space;=&space;1\\&space;-log(1-&space;\hat{p}),&space;y&space;=&space;0&space;\end{pmatrix}" /></p>

- 이 비용함수는 t가 0에 가까워지면 -log(t) 가 매우 커지므로 타당하다 할 수 있음
- 그러므로 모델이 양성 샘플을 0에 가까운 확률로 추정하면 비용이 크게 증가함
- 또한 음성 샘플을 1에 가까운 확률로 추정해도 비용이 크게 증가함
- 반면에 t가 1에 가까우면 -log(t)는 0에 가까워짐
- 따라서 기대한 대로 음성 샘플의 확률을 0에 가깝게 추정하거나 양성 샘플의 확률을 1에 가깝게 추정하면 비용은 0에 가까워질 것임
- <b>전체 훈련 세트에 대한 비용 함수는 모든 훈련 샘플의 비용을 평균한 것</b>  
  이를 로그 손실이라고 부르며, 다음과 같이 하나의 식으로 쓸 수 있음
<p align = 'center'><img src="  https://latex.codecogs.com/gif.latex?j(\theta)&space;=&space;-\frac{1}{m}\sum_{m}^{i=1}[y^{(i)}log(\hat{p^{i}})&space;&plus;&space;(1&space;-&space;y^{(i)})log(1&space;-&space;\hat{p^{(i)}})]" /></p>

- 안타깝게도 이 비용 함수의 최솟값을 계산하는 알려진 해가 없음(정규방정식 같은 것이 없음)
- 하지만 이 비용 함수는 볼록 함수이므로 경사 하강법(또는 어떤 다른 최적화 알고리즘)이 전역 최솟값을 찾는 것을 보장함(학습률이 너무 크지 않고 충분히 기다릴 시간이 있다면)
- 이 비용 함수의 j번째 모델 파라미터 theta(j)에 대해 편미분을 하면 다음 식과 같음
<p align = 'center'><img src="https://latex.codecogs.com/gif.latex?\frac{\sigma}{\sigma\theta}J(\theta)&space;=&space;\frac{1}{m}&space;\sum_{i&space;=&space;1}^{m}(\sigma(\theta^{T}x^{(i)})-&space;y^{(i)})&space;x_{j}^{(i)} " /></p>

- 각 샘플에 대해 예측 오차를 계산하고, j번쨰 특성값을 곱해서 모든 훈련 샘플에 대해 평균을 냄
- 모든 편도함수를 포함한 그레디언트 벡터를 만들면 경사 하강법 알고리즘을 사용할 수 있음
- 이 떄 확률적 경사 하강법과 미니배치 경사 하강법은 동일한 개념으로 적용됨
- 다른 선형 모델처럼 로지스틱 회귀 모델도 l1, l2 패널티를 사용하여 규제 가능

## 4.6.4 소프트맥스 회귀
- 로지스틱 회귀 모델은 여러 개의 이진 분류기를 훈련시켜 연결하지 않고 직접 다중 클래스를 지원하도록 일반화될 수 있음
- 이를 <b>소프트맥스 회귀</b>, <b>다항 로지스틱 회귀</b>라고 함
- 개념은 매우 간단한데, 샘플 x가 주어지면 소프트맥스 회귀 모델이 각 클래스 k에 대한 점수 sk(x)를 계산하고, 그 점수에 소프트맥스 함수를 적용하여 각 클래스의 확률을 추정
- 크로스앤트로피 비용 함수를 사용할 수 있음