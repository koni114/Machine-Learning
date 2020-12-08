## 의사결정트리(DecisionTree) 완전 정복 
### 의사결정트리 설명
* 하나의 설명변수를 사용하여 예측 가능한 규칙들의 집합을 생성하는 알고리즘인 의사결정트리
* 사람이 판단 가능한 특정 규칙에 의해서 최종 값을 예측.
* 계산 복잡도에 비해 성능이 좋지만, 결정경계가 데이터의 수직적이여서 특정 데이터에만 잘 작동할 가능성이 높음

### 불순도, 불확실성
* 영역을 나누는 기준
* 순도(homogeneity) 증가, 불순도(impurity), 불확실성(uncertainty)이 최대한 감소하도록 영역을 나눔
* 순도가 증가하고, 불순도 및 불확실성이 감소하는 것을 정보 이론에서는 Information gain 이라고 함
* 순도를 계산하는 방식 3가지에 대해서 알아보자

#### 엔트로피(entropy)
* 다음과 같은 식으로 정의됨(pk =  A 영역이 속하는 레코드 가운데 k 범주에 속하는 비율)
* 엔트로피가 감소하는 방식으로 tree를 split 함
$$ Entropy(A)=-\sum _{ k=1 }^{ m }{ { p }_{ k }\log _{ 2 }{ { (p }_{ k }) } } $$ 

#### 지니계수(Gini  Index)
$$ G.I(A)=\sum _{ i=1 }^{ d }{ { \left( { R }_{ i }\left( 1-\sum _{ k=1 }^{ m }{ { p }_{ ik }^{ 2 } } \right) \right) } } $$

### 모델 학습
* 의사결정나무의 학습 과정은 입력 변수 영역을 두 개로 구분하는 재귀적 분기(recursive partitioning)와 자세하게 구분된 영역을 통합하는 가지치기(pruning) 두 가지 과정으로 요약

#### 재귀적 분기
* 한 변수 기준으로 정렬
* 이후 가능한 모든 분기점에 대해 엔트로피/지니 계수를 구해 분기 전과 비교해 Information Gain을 계산
* 다른 변수도 위의 두 과정을 동일하게 진행
* 이 중에서 가장 Information Gain 값이 큰 분기점을 선택해 분기 수행
* 이러한 과정을 계속 반복(recursive)를 수행 해 분기를 수행
* 1회 분기를 위해 수행해야 하는 경우의 수 : 변수 v개, recode n개라고 하면, --> v(n-1) 번 만큼 수행

#### 가지치기
* 모든 terminal node의 순도가 100%인 tree를 Full Tree라고 하는데,  Full tree를 생성한 뒤 적절한 수준에서 terminal node를 결합해 주어야 함
* 가지치기의 비용함수(cost function)가 있는데, 이 비용함수를 최소로 하는 분기를 찾아내도록 학습됨 
* CC(T) : 의사결정나무의 비용 복잡도(= 오류가 적으면서, terminal node 수가 적은 단순한 모델일수록 작은 값)
* ERR(T) : 검증 데이터에 대한 오분류율
* L(T) : terminal node 수
* Alpha : ERR(T) 와 L(T) 를 결합하는 가중치(사용자에 의해 부여됨. 보통 0.1 ~ 0.01 사이의 값을 씀)
$$ CC(T)=Err(T)+\alpha \times L(T) $$ 


### 의사결정트리 종류
#### CTREE
* hyper parameter
  * min_split
    * 한 노드를 분할하기 위해서 필요한 데이터 개수 
    * default : 10
  * max_depth
    * 나무구조의 깊이 설정. 뿌리노드는 0, maxdepth = 5이면 나무구조는 뿌리구조에서 5단계 내려감. 
    * default : 10	
  * minbucket 
    * 최종 노드에 포함되어야 할 데이터의 최소 개수
  * cp 
    * 비용복잡함수의 벌점 모수. 노드를 분할 할 때 분할 전과 비교하여 오분류율이 cp값 이상으로  
    향상되지 않으면 더 이상 분할하지 않고 나무 구조 생성을 멈춤. 
    * default : 0.01  

#### CART:RPART
*  rpart 패키지에서는 cp값을 증가시켜가며 tree 크기를 감소시켜 x validation error(xerror)을 계산
* xerror이 최소로 하는 cp가 최적
* hyper parameter
  * min_split
    * 한 노드를 분할하기 위해서 필요한 데이터 최소 개수 
  * xval
    * 교차타당성의 fold 개수, 디폴트는 10 
  * cp
    *  비용복잡함수의 벌점모수. 노드를 분할할 때 분할 전과 비교하여 
     오분류율이 cp 값 이상으로 향상되지 않으면 더 이상 분할하지 않고 나무구조 생성을 멈춤. 디폴트는 0.01
  * nsplit 
    * 가지의 분기수. nsplist + 1 만큼의 leaf node 생성. 

#### C50
* hyper paramter
  *  Winnowing
     * 입력 필드에 대해서 사전에 필드가 유용한지 측정한 다음 유용하지 않는 경우 배제하고 모델링
  *  globalPrunning
     *  전역적 가지치기 여부를 결정
     * 전역적 가지치기는 전체적으로 만들어진 Tree 구조에서  
     가지치기를 수행하는데 강도가 약한 sub-tree자체를 삭제
  * earlyStopping
    * 성능이 더이상 좋아지지 않으면 modeling stop.


### Caret :: DecisionTree
#### CTREE
*  parameter : cp
   * The complexity parameter (cp) is used to control the size of the decision tree and to select the optimal tree size.
#### RPART
* parameter : mincriterion
  * the value of the test statistic (for testtype == "Teststatistic"),  
    or 1 - p-value (for other values of testtype) that must be exceeded in order to implement a split.
    mincriterion = 0.95
#### C50
* parameter  :  trials, model, winnow
  * model : 'tree', 'rules'
