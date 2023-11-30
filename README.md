# [23.06] 캐글 Identifying Age-Related Conditions(의료)

![Untitled](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/582184b7-33d7-4891-8bdb-67b5ffe13701 /assets/73885257/dc779507-5c9b-49da-a0b9-f8ee4b95eb6c![image](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/023e5e96-b6f0-4274-a48c-c3a2a7c0fe01)
)

- 프로젝트 목표
    
    : 사람이 세 가지 의료 상태 중 하나 이상을 가지고 있는지 (Class 1) 또는 세 가지 의료 상태 중 아무것도 가지고 있지 않은지 (Class 0)를 예측하는 머신모델 개발
    

- 데이터
    
    : 56개 피쳐를 가진 Train data + 5개의 피쳐를 가진 메타데이터(greek)
    
    - 해당 피쳐들은 보완을 위해 공개되지 않으며, 메타데이터 내 Epsilon 피쳐는 정보를 수집한 날짜에 해당함.

- 기간
    
    : 23.06.19 ~ 23.06.29
    

- 강사 피드백
    
    ![Untitled](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/2afbe9f3-06b7-4c01-8f13-72ab64d23ec7![image](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/94970dc2-b175-42bd-9325-a0b520dd5349)
)
    

    

## 1.  프로젝트 관리 세팅

- 캐글 대회의 개인 제출 특성상 팀프로젝트이더라도 개인프로젝트처럼 진행될 요소가 있어 팀 구성의 이점을 살리고자 프로젝트 관리 세팅을 우선적으로 진행

![Untitled](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/119065f3-f320-410e-936e-a2285580dc44![image](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/3d198628-469b-44ab-9897-26ebfa23902e)
)

- 2가지 원칙을 통해 방향성 수립
    1. 대회에서 공개된 다른 유저의 code를 참조 및 사용하되 확실히 이해한 것만 사용할 것!
    2. 이해한 코드라면 가져올 때, 그대로 복사하지말고 우리 팀의 베이스코드에 추가할 것!
- 팀마다 주어지는 강사님 피드백시간이 짧으므로 그전 내부회의 및 회의록 작성을 통해 깔끔하게 정리하여 피드백시간 최대한 활용
- 개개인이 캐글 플랫폼에 제출하여 점수를 받아본 코드들은 서로 공유하는 공간을 만들어 비슷한 시행착오 방지
- 세부페이지
    
    ![Untitled](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/10c323b8-c545-47f4-8b31-83a8a3e753c6![image](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/60e72f05-2b31-4b4c-89b4-2211d0ebcc03)
)
    
    ![Untitled](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/53ec2299-e716-4820-8a0a-b4ffac8eeea2![image](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/7cc75e49-1450-4f35-a794-74c74be8bc3d)
)
    

## 2.  탐색적 데이터분석(EDA)

### 1) 평가지표(Balanced logloss) 분석

---

- Logloss는 다른 평가지표와 비교했을 때, 우연히 정답을 맞추는 것을 방지하기 위해 자신있게 틀린 값에 대해 큰 페널티를 줌.
    
    ![Untitled](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/1ce74bdd-cc20-43e9-9de7-ecdb263dc81a![image](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/4266726e-38fe-4b32-ba5c-a23fcb82a500)
)
    
    ![Untitled](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/6dbad440-0e31-4693-9eb3-51cf5fb13f93![image](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/03bc1469-a864-4a85-8a77-a151b4539c31)
)
    
    - 수식에서 보면 -log(확률값) 형태로 구성됨.
        - 기존의 0과 가까워질 때 값이 급격히 떨어지는 로그 함수의 특성을 반대(-)로 활용하여 페널티를 높임.
- 위에까지는 logloss의 특징이며, 현재 프로젝트의 학습(train) 데이터에서 Class(0, 1)별로 데이터가 균등하게 분포되지 않아 데이터가 많은 Class로 예측하게 되는 경향이 있음.
- 그래서 대회의 평가지표로 이를 보정할 수 있는 Balanced logloss를 활용함.
    
    ![Untitled](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/b65e2249-fb0f-4ff1-b237-55a4df1ec0f8![image](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/d3438b37-2d09-4e8a-aefc-bb2165c52c33)
)
    

### 2) 데이터

---

- 의료 데이터를 다루는 대회 특성상 각 feature 들이 어떤 항목인지 알 수 없음.
- Train 데이터 분석
    - 총 56의 건강지표(feature)

![Untitled](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/23cfcb68-c509-4c10-abc3-b04b48e37b18![image](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/096cbbc6-5c56-460a-9555-38ef45cb0aa2)
)

![Untitled](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/31574c7a-![image](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/4cc32220-41ba-4b24-9c1c-1e5300e9c512)
)

→ 일부 보정을 줘서 추정했을 때, BN Feature는 나이와 같이 보임

- greek 데이터 분석
    - 4개의 feature(Alpha, Beta, Gamma, Delta) + data 수집 일을 나타내는 1개의 feature(Epsilon)
        - 일자 데이터인 Epsilon을 제외하고 Age-related data임.
            
            ![Untitled](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/e0d68160-4980-45d7-9d96-6983487da9ff![image](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/a6632d82-ee0e-4046-b91b-fb17ca1299c1)
)
            
    - Alpha, Gamma는 class 0, 1로 분류했을 때 겹치는 부분이 없이 나눠지는 것으로 보아 하위카테고리로 에측 가능함.

### 3) 도메인 분석

---

- ICR 홈페이지

![Untitled](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/015f274a-b816-4fd2-9edb-cea91902c9ba![image](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/f37373b8-c059-4315-897a-79bdafe95a7c)
)

→ 위에서 도출한 인사이트로 봤을 때, class 내 하위카테고리가 존재하며, Class별 나이(BN)를 봤을 때, 큰 차이를 보이지 않았음으로 ICR 연구 중 질환에 관련된 연구가 아닌 유전자 등 사람의 고유형질을 나타내는 ‘Age-related Immune Senscence’, ‘In Vitro Diagnostics and Biomarkers’ 가 주제임을 추측할 수 있음. 

- 위 힌트들을 참고하여 ChatGPT와 항목을 찾았봤으나 의미있지 않았음.
    
    ![Untitled](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/207964f1-14ed-4961-b871-2ba09d69a8bf![image](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/3827cae2-9a7c-4e2d-8249-681ec2850f15)
)
    

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
            
            ![Untitled](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/ba8155cb-ff2a-4fe5-a78b-1f46173da64b![image](https://github.com/jun-suk/PJT_kaggle_icr/assets/73885257/2843feac-d8df-4a87-a87b-7e06a1cf3264)
)
      
                
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
