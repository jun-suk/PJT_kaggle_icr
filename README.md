# [23.06] 캐글 Identifying Age-Related Conditions(의료)

![Untitled](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/Untitled.png)

- 프로젝트 목표
    
    : 사람이 세 가지 의료 상태 중 하나 이상을 가지고 있는지 (Class 1) 또는 세 가지 의료 상태 중 아무것도 가지고 있지 않은지 (Class 0)를 예측하는 머신모델 개발
    

- 데이터
    
    : 56개 피쳐를 가진 Train data + 5개의 피쳐를 가진 메타데이터(greek)
    
    - 해당 피쳐들은 보완을 위해 공개되지 않으며, 메타데이터 내 Epsilon 피쳐는 정보를 수집한 날짜에 해당함.

- 기간
    
    : 23.06.19 ~ 23.06.29
    

- 강사 피드백
    
    ![Untitled](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/Untitled%201.png)
    

- 발표자료
    
    [[머신러닝 팀프] 발표자료_4팀_ver.4 (2).pdf](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/%25E1%2584%2586%25E1%2585%25A5%25E1%2584%2589%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2585%25E1%2585%25A5%25E1%2584%2582%25E1%2585%25B5%25E1%2586%25BC_%25E1%2584%2590%25E1%2585%25B5%25E1%2586%25B7%25E1%2584%2591%25E1%2585%25B3_%25E1%2584%2587%25E1%2585%25A1%25E1%2586%25AF%25E1%2584%2591%25E1%2585%25AD%25E1%2584%258C%25E1%2585%25A1%25E1%2584%2585%25E1%2585%25AD_4%25E1%2584%2590%25E1%2585%25B5%25E1%2586%25B7_ver.4_(2).pdf)
    

## 1.  프로젝트 관리 세팅

- 캐글 대회의 개인 제출 특성상 팀프로젝트이더라도 개인프로젝트처럼 진행될 요소가 있어 팀 구성의 이점을 살리고자 프로젝트 관리 세팅을 우선적으로 진행

![Untitled](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/Untitled%202.png)

- 2가지 원칙을 통해 방향성 수립
    1. 대회에서 공개된 다른 유저의 code를 참조 및 사용하되 확실히 이해한 것만 사용할 것!
    2. 이해한 코드라면 가져올 때, 그대로 복사하지말고 우리 팀의 베이스코드에 추가할 것!
- 팀마다 주어지는 강사님 피드백시간이 짧으므로 그전 내부회의 및 회의록 작성을 통해 깔끔하게 정리하여 피드백시간 최대한 활용
- 개개인이 캐글 플랫폼에 제출하여 점수를 받아본 코드들은 서로 공유하는 공간을 만들어 비슷한 시행착오 방지
- 세부페이지
    
    ![Untitled](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/Untitled%203.png)
    
    ![Untitled](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/Untitled%204.png)
    

## 2.  탐색적 데이터분석(EDA)

### 1) 평가지표(Balanced logloss) 분석

---

- Logloss는 다른 평가지표와 비교했을 때, 우연히 정답을 맞추는 것을 방지하기 위해 자신있게 틀린 값에 대해 큰 페널티를 줌.
    
    ![Untitled](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/Untitled%205.png)
    
    ![Untitled](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/Untitled%206.png)
    
    - 수식에서 보면 -log(확률값) 형태로 구성됨.
        - 기존의 0과 가까워질 때 값이 급격히 떨어지는 로그 함수의 특성을 반대(-)로 활용하여 페널티를 높임.
- 위에까지는 logloss의 특징이며, 현재 프로젝트의 학습(train) 데이터에서 Class(0, 1)별로 데이터가 균등하게 분포되지 않아 데이터가 많은 Class로 예측하게 되는 경향이 있음.
- 그래서 대회의 평가지표로 이를 보정할 수 있는 Balanced logloss를 활용함.
    
    ![Untitled](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/Untitled%207.png)
    

### 2) 데이터

---

- 의료 데이터를 다루는 대회 특성상 각 feature 들이 어떤 항목인지 알 수 없음.
- Train 데이터 분석
    - 총 56의 건강지표(feature)

![Untitled](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/Untitled%208.png)

![Untitled](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/Untitled%209.png)

→ 일부 보정을 줘서 추정했을 때, BN Feature는 나이와 같이 보임

- greek 데이터 분석
    - 4개의 feature(Alpha, Beta, Gamma, Delta) + data 수집 일을 나타내는 1개의 feature(Epsilon)
        - 일자 데이터인 Epsilon을 제외하고 Age-related data임.
            
            ![Untitled](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/Untitled%2010.png)
            
    - Alpha, Gamma는 class 0, 1로 분류했을 때 겹치는 부분이 없이 나눠지는 것으로 보아 하위카테고리로 에측 가능함.

### 3) 도메인 분석

---

- ICR 홈페이지

![Untitled](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/Untitled%2011.png)

→ 위에서 도출한 인사이트로 봤을 때, class 내 하위카테고리가 존재하며, Class별 나이(BN)를 봤을 때, 큰 차이를 보이지 않았음으로 ICR 연구 중 질환에 관련된 연구가 아닌 유전자 등 사람의 고유형질을 나타내는 ‘Age-related Immune Senscence’, ‘In Vitro Diagnostics and Biomarkers’ 가 주제임을 추측할 수 있음. 

- 위 힌트들을 참고하여 ChatGPT와 항목을 찾았봤으나 의미있지 않았음.
    
    ![Untitled](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/Untitled%2012.png)
    

## 3.  모델 구현 (Score 0.23) - 1주차

- 모델 선택
    - Voting Ensemble을 통해 각기 다른 특성을 가진 Random Forest(배깅), SVM, XGBT(부스팅), TabPFN(딥러닝)을 사용했으며, 성능 확인 후 XGBT+TabPFN을 최종 사용
        - TabPFN은 정형데이터인 작은 데이터셋과 시계열을 다루는 딥러닝 모델
- CV 평가
    - 작은데이터에서는 학습과정에서 평가가 중요하며, 그 점수가 충분한 객관성을 갖고, 캐글 제출 점수와 유사하게 나와야 함으로 여러번 평가를 진행하는 CV를 이용함.
- 데이터를 가공하는 작업은 아래와 같은 것들을 실험했으나 자체 전처리가 포함된 딥러닝(TabPFN) 특성에 따라 최종적으로 쓰지 않음.
    - 실험한 기법들
        - Scaler
            - MINMAX, Standard, Robust, Quantile transformer
        - Sampling
            - Under, Over(Random over, SMOTE, ADASYN), Hybrid
        - Feature selection
            - 모델 Feature importance, Permutation
        - Feature extraction(차원축소)
            - PCA, LDA
        - Class Imbalance
            - 모델 내 파라미터인 is_unbalance=True, scale_pos_weright, class_weight=”balacnced”

## 4. 결론 (Score 0.11) - 2주차

- 2주차에는 public에 있는 코드를 참조하여 인사이트를 얻었고, 베이스코드에 추가하여 최종 0.11의 Score를 달성하였다.
    - Alpha 예측 후 베이지안 통계기법 사용
        - Alpha를 예측한 후, Class개수로 나눠준 후, 한 관측 데이터(row)당 확률이 합쳐서 1일 될 수 있도록 보정해준다.
            
            ![Untitled](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/Untitled%2013.png)
            
            - Alpha 예측값을 prior로 두고, Class 예측값을 환산(Posterior)한 베이지안 통계 기법
                
                ![Untitled](%5B23%2006%5D%20%E1%84%8F%E1%85%A2%E1%84%80%E1%85%B3%E1%86%AF%20Identifying%20Age-Related%20Conditions(%E1%84%8B%201eacf0ef282e4a629ae6e3a5c26e6594/Untitled%2014.png)
                
    - Epsilon 사용
        - Test 데이터의 수집 일자가 Train보다 늦다는 정보를 대회측에서 제공해 줬으므로, Test 데이터에 Train 데이터 중 가장 늦게 수집된 데이터 + 1의 날짜를 일괄적으로 기입해줌.
        
         
        
- 위 사항으로 유추할 수 있는 것
    1. 일반적으로 Train 데이터에서 이상치에 해당하는 값들이 성능을 높이고, 분류에 도움이 됨.
        - 우리가 볼 수 없는 test 데이터(score를 내는)에서는 해당 범위가 이상치가 아닐 가능성이 높음
    2. 모델로 Class를 예측하지 않고, Alpha를 예측해서 베이지안 통계 확률 구하는 방식처럼(Alpha 예측에서 나온 확률을 prior로 두고 계산) 구하는 것이 imbalance 해결에 도움을 줌.
        - test 데이터셋에서 Alpha 분포는 traint셋과 유사하지만 Class는 그렇지 않을 가능성 높음.
    3. Epsilon(일자 정보)이 결측치가 많음에도 포함했을 때, 성능이 많이 늘어남.
        - 위 예측 중 질병발병이 아닌 바이오마커 등에 항목이라는 예측이 맞다면, 동일 실험군에 여러번(다른시기에) 실험을 했으나 이를 다른 사람처럼 보이게 ID가 부여되었을 가능성이 있음.
        - 혹은 시기에 따라 실험군 특성을 다르게 했을 가능성이 있다.