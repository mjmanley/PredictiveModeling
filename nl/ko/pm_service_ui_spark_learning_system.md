---

copyright:
  years: 2016, 2017
lastupdated: "2017-09-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 연속 학습 시스템 <span class='tag--beta'>베타</span>

IBM® Watson™ Machine Learning 연속 학습 시스템에서는 예측 품질을 위해 모델 성능, 재교율 및 재배치를 자동으로 모니터링합니다.

**시나리오 이름**: 심장병 치료용으로 선택할 수 있는 최고의 약물.

**시나리오 설명**: 심장병 치료 약물을 생산하는 생물 의학 회사에서 최고의 심장병 치료 약물을 선택하는 모델을 배치하고자 합니다. 약물 효과에 관한 새로은 증거가 생기면 모델 업데이트를 고려해야 합니다. 데이터 과학자는 예측 모델을 준비하고 사용자(개발자)와 이를 공유합니다. 수행해야 할 태스크는 모델을 배치하고, 학습 구성을 설정하며, 학습 반복을 실행하여 모델을 평가, 재훈련 및 재배치하는 것입니다.

## 샘플 모델 사용

1. IBM® Watson™ Machine Learning 대시보드의 샘플 탭으로 이동하십시오. 

2. 샘플 모델 섹션에서 심장병 약물 선택 타일을 찾고
   모델 추가 단추(+)를 클릭하십시오. 

이제 모델 탭의 사용 가능한 모델 목록에 샘플 심장병 약물 선택 모델이 표시됩니다. 


## 공개된 모델의 연속 학습 시스템 설정

1.  IBM® Watson™ Machine Learning 대시보드의 모델 탭으로 이동하십시오. 

2.  **조치** 메뉴에서 **세부사항 보기**를 클릭하십시오.

3.  **재훈련 세부사항**으로 화면이동하여 **편집**을 누르십시오.

4.  다음 항목을 제공해야 합니다. 

    **피드백 연결**: 모델 평가 및 재훈련의 입력(피드백 데이터)으로 사용될 Db2 Warehouse on Cloud 세부사항입니다.
    
    ```
    {
        "connection": {
      "username": "dash102204",
            "host": "awh-yp-small02.services.dal.bluemix.net",
            "password": "NweTlYwPY6cu",
            "db": "BLUDB"
        },
    "source": {
      "type": "dashdb",
            "tablename": "DRUG_FEEDBACK_DATA"
        }
    }
    ```
    {: codeblock}

    다음 지시사항을 사용하여 Db2 Warehouse on Cloud에서 `DRUG_FEEDBACK_DATA` 테이블을 준비하십시오. 
    - [Db2 Warehouse on Cloud Service](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/) 인스턴스를 작성하십시오(시작 플랜은 제공됨).
    - **Db2 Warehouse on Cloud**에 **DRUG_FEEDBACK_DATA** 테이블을 작성하십시오.
      + git 저장소에서 [drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv) 파일을 다운로드하십시오.
      + **콘솔 열기**를 클릭하여 **Db2 Warehouse on Cloud** 아이콘을 시작하십시오.
      + **데이터 로드** 및 **데스크탑** 로드 유형을 선택하십시오.
      + 이전에 다운로드한 파일에 대해 **끌어서 놓기**를 수행하고 **다음**을 누르십시오.
      + **스키마**를 선택하여 데이터를 가져오고 **새 테이블**을 클릭하십시오.
      + **새 테이블**의 이름을 쓴 후 **다음**을 클릭하여 데이터 가져오기를 완료하십시오.
      + `;`을 **필드 구분 기호**로 사용하십시오.
      + 업로드된 데이터로 테이블을 작성하려면 **다음**을 클릭하십시오.

    **참고**: 이 [REST API 엔드포인트](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback)를 사용하여 피드백 데이터베이스에 새로운 피드백 레코드를 추가할 수 있습니다.

    **최소 데이터 크기**: 모델 평가를 시작할 피드백 데이터 세트의 최소 레코드 수입니다(학습 시스템 반복의 일부).

    ```
    20
    ```
    {: codeblock}

    **Spark 연결**: Spark 서비스 신임 정보는 Bluemix Spark 서비스 대시보드의 서비스 신임 정보 탭에 있습니다.

    ```
{
    "credentials":{
      "tenant_id": "s745-299dcf850a6390-35c9a7ecf27a",
      "tenant_id_full": "ba3dde5a-ee64-4057-9749-299dcf850a63_4c55eb1c-d6fe-4f0a-9390-35c9a7ecf27a",
      "cluster_master_url": "https://spark.bluemix.net",
      "instance_id": "ba3dde5a-ee64-4057-9749-299dcf850a63",
      "tenant_secret": "c0cba7a4-7b19-46e6-9326-44c4f48aaf08",
      "plan": "ibm.SparkService.PayGoPersonal"
    },
    "version":"2.0"
}
    ```
    {: codeblock}

    **임계값**: 재훈련 프로세스를 트리거하는 임계값입니다(평가 중에 계산된 경우 메트릭 값은 임계값 미만임).

    ```
    0.8
    ```

    **재훈련된 모델 자동 배치**: 현재 배치된 모델보다 품질(메트릭 값)이 우수한 것으로 표시되면 재훈련된 모델을 배치하십시오.

5.  **설정**을 클릭하십시오.


## 연속 학습 시스템 반복 실행

반복하는 동안 공개된 모델을 평가합니다. 평가된 정확도가 지정된 임계값 미만이면 모델 재훈련이 트리거됩니다. 두 데이터 세트: 훈련 및 피드백 모두 재훈련과 평가에 사용됩니다.

1. 새 반복을 시작하려면 모델 **세부사항** 양식의 **모니터** 탭에서 **평가**를 클릭하십시오.

3. 반복 결과를 확인하려면 평가 이벤트 테이블 또는 차트 보기로 이동하십시오. 여기에서 피드백 데이터(모니터링), 재훈련된 모델 품질(작성되어 평가된 새 모델 버전)을 기반으로 계산된 모델 품질에 대한 정보를 찾을 수 있습니다. 

4. 자동으로 훈련된 모델 목록과 해당 품질을 보려면 개요 탭(모델 세부사항 보기 > 개요)의 맨 아래에 있는 버전 히스토리로 이동하십시오.
