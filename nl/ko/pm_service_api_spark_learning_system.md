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

연속 학습 시스템에서는 올바른 예측 품질을 위해 모델 성능, 재교율 및 재배치를 자동으로 모니터링합니다.


**시나리오 이름**: 심장병 치료용으로 선택할 수 있는 최고의 약물.

**시나리오 설명**: 심장병 치료 약물을 생산하는 생물 의학 회사에서
최고의 심장병 치료 약물을 선택하는 모델을 배치하고자 합니다. 약물 효과에 관한 새로은 증거가 생기면 모델 업데이트를 고려해야 합니다. 
데이터 과학자는 예측 모델을 준비하고 이를 사용자(개발자)와 공유합니다. 수행해야 할 태스크는 모델을 배치하고, 학습 구성을 설정하며, 학습 반복을 실행하여 모델을 평가, 재훈련 및 재배치하는 것입니다.

**참고**: 샘플 모델을 작성하고 학습 시스템을 구성하며 최종적으로 학습 반복을 실행하는 python [notebook](https://apsportal.ibm.com/analytics/notebooks/a97cde0b-5bb8-436a-ae82-83e96adc45e0/view?access_token=6baf4c722e452836f7b505205bc96d9a24b9333ee9b5c39453f6d7751987f798)도 사용할 수 있습니다.

## 샘플 모델 사용

1. IBM® Watson™ Machine Learning 대시보드의 **샘플** 탭으로 이동하십시오. 

2. **샘플 모델** 섹션에서 심장병 약물 선택 타일을 찾아 **모델 추가** 아이콘(+)을 클릭하십시오.

이제 모델 탭의 사용 가능한 모델 목록에 샘플 심장병 약물 선택 모델이 표시됩니다. 

## 액세스 토큰 생성

IBM Watson Machine Learning 서비스 인스턴스의 서비스 신임 정보 탭에서 사용 가능한 사용자 및
비밀번호를 사용하여 액세스 토큰을 생성하십시오. 

요청 예제: 

```
curl --basic --user <username>:<password> https://ibm-watson-ml.mybluemix.net/v3/identity/token
```
{: codeblock}

출력
예제: 

```
{"token":"**********"}
```
{: codeblock}

환경 변수 토큰에 토큰 값을 지정하려면 다음 터미널
명령을 사용하십시오.

```
token="<token_value>"
```
{: codeblock}

## 공개된 모델에 대해 작업

다음 API 호출을 사용하여 다음과 같은 인스턴스 세부 사항을 가져오십시오.

* 공개된 모델 `url`
* 배치 `url`
* 사용 정보

요청 예제: 

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}
```
{: codeblock}

출력
예제: 

```
{
   "metadata":{
      "guid":"360c510b-012c-4793-ae3f-063410081c3e",
      "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e",
      "created_at":"2017-08-04T09:15:48.344Z",
      "modified_at":"2017-08-22T08:34:47.759Z"
   },
   "entity":{
      "source":"Bluemix",
      "published_models":{
         "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/published_models"
      },
      "usage":{
         "expiration_date":"2017-09-01T00:00:00.000Z",
         "computation_time":{
            "current":4
         },
         "model_count":{
            "limit":1000,
            "current":2
         },
         "prediction_count":{
            "current":16
         },
         "deployment_count":{
            "limit":1000,
            "current":1
         }
      },
      "plan_id":"0f2a3c2c-456b-40f3-9b19-726d2740b11c",
      "status":"Active",
      "organization_guid":"b0e61605-a82e-4f03-9e9f-2767973c084d",
      "region":"us-south",
      "account":{
         "id":"f52968f3dbbe7b0b53e15743d45e5e90",
         "name":"Umit Cakmak's Account",
         "type":"TRIAL"
      },
      "owner":{
         "ibm_id":"31000292EV",
         "email":"umit.cakmak@pl.ibm.com",
         "user_id":"43e0ee0e-6bfb-48fc-bcd8-d61e40d19253",
         "country_code":"POL",
         "beta_user":true
      },
      "deployments":{
         "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/deployments"
      },
      "space_guid":"4c55eb1c-d6fe-4f0a-9390-35c9a7ecf27a",
      "plan":"standard"
   }
}
```
{: codeblock}


**published_models** `url`이 있으므로 다음 API 호출을 사용하여 모델의 세부사항을 가져오십시오.

요청 예제: 

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer  $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models
```
{: codeblock}

출력
예제: 

```
{  
   "count":1,
   "resources":[  
      {  
         "metadata":{
      "guid":"361d0edb-c5c9-4b8c-b353-d968e7dc0b8d",
            "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/published_models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d",
            "created_at":"2017-08-22T08:34:47.597Z",
            "modified_at":"2017-08-22T08:34:47.691Z"
         },
   "entity":{
      "runtime_environment":"spark-2.0",
            "author":{  

            },
            "name":"Best Heart Drug Selection",
            "label_col":"DRUG",
            "training_data_schema":{  
               "fields":[  
                  {  
                     "metadata":{
      "scale":0,
                        "name":"AGE"
                     },
                     "type":"integer",
                     "name":"AGE",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":0,
                        "name":"SEX"
                     },
                     "type":"string",
                     "name":"SEX",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":0,
                        "name":"BP"
                     },
                     "type":"string",
                     "name":"BP",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":0,
                        "name":"CHOLESTEROL"
                     },
                     "type":"string",
                     "name":"CHOLESTEROL",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":6,
                        "name":"NA"
                     },
                     "type":"decimal(12,6)",
                     "name":"NA",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":6,
                        "name":"K"
                     },
                     "type":"decimal(13,6)",
                     "name":"K",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":0,
                        "name":"DRUG"
                     },
                     "type":"string",
                     "name":"DRUG",
                     "nullable":true
                  }
               ],
               "type":"struct"
            },
            "latest_version":{  
               "url":"https://ibm-watson-ml.mybluemix.net/v2/artifacts/models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d/versions/8dfe9548-57ec-4768-8d3e-6c1e7e5cdfc3",
               "guid":"8dfe9548-57ec-4768-8d3e-6c1e7e5cdfc3",
               "created_at":"2017-08-22T08:34:47.691Z"
            },
            "model_type":"sparkml-model-2.0",
            "deployments":{  
               "count":0,
               "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/published_models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d/deployments"
            },
            "input_data_schema":{  
               "fields":[  
                  {  
                     "metadata":{
      "scale":0,
                        "name":"AGE"
                     },
                     "type":"integer",
                     "name":"AGE",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":0,
                        "name":"SEX"
                     },
                     "type":"string",
                     "name":"SEX",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":0,
                        "name":"BP"
                     },
                     "type":"string",
                     "name":"BP",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":0,
                        "name":"CHOLESTEROL"
                     },
                     "type":"string",
                     "name":"CHOLESTEROL",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":6,
                        "name":"NA"
                     },
                     "type":"decimal(12,6)",
                     "name":"NA",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":6,
                        "name":"K"
                     },
                     "type":"decimal(13,6)",
                     "name":"K",
                     "nullable":true
                  }
               ],
               "type":"struct"
            }
         }
      }
}
```
{: codeblock}


## 공개된 모델의 연속 학습 시스템 설정

이 하위 섹션에서는 사용자의 모델에 맞게 연속 학습 시스템을 구성하는 방법을 알아봅니다.

### 권한 헤더 준비

Watson Machine Learning 토큰 및 Spark 인스턴스 신임 정보를 결합하는 권한 헤더를 준비하려면 다음 세부사항을 제공하십시오.

*  이전 단계에서 작성된 액세스 토큰
*  Spark 서비스 신임 정보는 Bluemix Spark 서비스 대시보드의 서비스 신임 정보 탭에서
찾을 수 있습니다. 배치 요청을 작성하기 전에 Spark 신임 정보를 base64로 인코딩해야 합니다. 이 정보는 X-Spark-Service-Instance 필드의 요청 헤더로 전달됩니다.

   사용 중인 운영 체제에 따라서 base64 인코딩을 수행한 다음 환경 변수에 지정하려면 다음 터미널 명령 중 하나를 실행해야 합니다. 

   macOS 운영 체제에서 다음 명령을 사용하십시오. 

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64)
   ```
   {: codeblock}

   Microsoft Windows 또는 Linux 운영 체제에서는 base64 인코딩을 수행하려면 `base64` 명령과 함께 `--wrap=0` 매개변수를 사용해야 합니다.

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64 --wrap=0)
   ```
   {: codeblock}


### 피드백 데이터 세트 준비

학습 시스템에서는 훈련 데이터(모델 훈련에 사용되는 데이터) 외에도 피드백 데이터(훈련된 모델을 평가하는 데 사용하는 데이터)에 연결해야 합니다. 아래 지시사항을 사용하여 **Db2 Warehouse on Cloud**에 **DRUG_FEEDBACK_DATA** 테이블을 준비하십시오.

- [Db2 Warehouse on Cloud Service](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/) 인스턴스를 작성하십시오(시작 플랜은 제공됨).
- **Db2 Warehouse on Cloud**에 **DRUG_FEEDBACK_DATA** 테이블을 작성하십시오.
  + git 저장소에서 [drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv) 파일을 다운로드하십시오.
  + **콘솔 열기**를 클릭하여 **Db2 Warehouse on Cloud** 아이콘을 시작하십시오.
  + **데이터 로드** 및 **데스크탑** 로드 유형을 선택하십시오.
  + 이전에 다운로드한 파일에 대해 **끌어서 놓기**를 수행하고 **다음**을 누르십시오.
  + **스키마**를 선택하여 데이터를 가져오고 **새 테이블**을 클릭하십시오.
  + **새 테이블** 필드에서 이름을 입력하고 **다음**을 클릭하십시오.
  + **필드 구분 기호**로 세미콜론(;)을 사용하십시오.
  + 업로드된 데이터로 테이블을 작성하려면 **다음**을 클릭하십시오.

**참고**: 이 [REST API 엔드포인트](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback)를 사용하여 피드백 데이터베이스에 새로운 피드백 레코드를 추가할 수 있습니다.

### 구성 페이로드 준비

학습 구성을 지정하려면 다음 엔드포인트를 사용해야 합니다.

```
https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_configuration
```
   {: codeblock}


다음 필드의 값을 정의하여 페이로드를 완료하십시오.

* `min_feedback_data_size` - 연속 학습 시스템 반복을 시작할 피드백 데이터 세트에 있는 최소 레코드 수입니다.
* `auto_retrain` [never, always, conditionally] - 이 매개변수는 재훈련 프로세스를 트리거해야 하는 시기를 지정합니다. [conditionally]는 모델 품질이 지정된 임계값 미만일 때 재훈련 프로세스를 트리거합니다.
* `auto_redeploy` [never, always, conditionally] - 이 매개변수는 재훈련 모델을 배치해야 하는 시기를 지정합니다. [conditionally]는 새로 훈련된 모델 품질이 현재 배치된 품질보다 우수할 때 모델 재배치를 트리거합니다.


요청 예제: 

```
curl -v -X PUT \
    -H "Content-Type:application/json" \
    -H "Authorization: Bearer $token" \
    -H "X-Spark-Service-Instance: $spark_credentials" \
    -d '{
          "definition": {
            "method": "binary",
            "metrics": [
              {
                "name": "areaUnderROC",
        "threshold": 0.8
      }
    ]
          },
          "feedback_data_ref": {
           "connection": {
      "db": "BLUDB",
            "host": "awh-yp-small02.services.dal.bluemix.net",
            "username": "dash102204",
            "password": "NweTlYwPY6cu"
           },
    "source": {
      "tablename": "DRUG_FEEDBACK_DATA",
            "type": "dashdb"
           }
          },
          "min_feedback_data_size": 100,
          "auto_retrain": "conditionally",
          "auto_redeploy": "conditionally",
          "schedule": {
            "expression": "0/15 * * * * ? *",
            "start": "2017-02-01T10:11:12Z",
            "until": "2017-06-01T10:11:12Z"
          },
          "last_training_record": 0
        }' \
    https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_configuration
```

{: codeblock}

출력
예제: 
```
{
   "min_feedback_data_size":100,
   "auto_retrain":"conditionally",
   "schedule":{
      "expression":"0/15 * * * * ? *",
      "start":"2017-02-01T10:11:12Z",
      "until":"2017-06-01T10:11:12Z"
   },
   "definition":{
      "method":"binary",
      "metrics":[
         {
            "name": "areaUnderROC",
        "threshold": 0.8
      }
    ]
   },
      "spark_service":{
         "credentials":{
            "tenant_id":"s971-2eeb9ffe2a3090-35c9a7ecf27a",
         "cluster_master_url":"https://spark.bluemix.net",
         "tenant_id_full":"55f1492d-b385-4fdd-b971-2eeb9ffe2a30_4c55eb1c-d6fe-4f0a-9390-35c9a7ecf27a",
         "tenant_secret":"5e7fc568-e94e-4689-b623-fe62e9ceedd2",
         "instance_id":"55f1492d-b385-4fdd-b971-2eeb9ffe2a30",
         "plan":"ibm.SparkService.PayGoPersonal"
      },
         "version":"2.0"
      },
   "feedback_data_ref":{
      "connection":{
         "db":"BLUDB",
         "host":"awh-yp-small02.services.dal.bluemix.net",
         "username":"dash102204",
         "password":"NweTlYwPY6cu"
      },
      "source":{
         "tablename":"DRUG_FEEDBACK_DATA",
         "type":"dashdb"
      }
   },
   "auto_redeploy":"conditionally"
}
```
{: codeblock}

**참고**: 이 예에서 `auto_retrain` 및 `auto_redeploy` 매개변수의 기본값을 사용합니다. 이러한 매개변수에 대한 자세한 정보는 `learning_configuration` 매개변수에 대한 [REST API 문서](http://watson-ml-api.mybluemix.net/#!/Published32Models/put_v3_wml_instances_instance_id_published_models_published_model_id_learning_configuration)에 있습니다.

## 연속 학습 시스템 반복 실행

학습 시스템 반복을 시작하려면 아래 표시된 REST API 메소드를 사용하십시오. 반복하는 동안 공개된 모델을 평가합니다. 평가된 정확도가 지정된 임계값 미만이면 모델 재훈련이 트리거됩니다. 두 데이터 세트: 훈련 및 피드백 모두 재훈련과 평가에 사용됩니다.

요청 예제: 

```
curl -X POST --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

출력
예제: 

```
요청이 이행되었으므로 새로운 리소스가 작성됩니다.
```
{: codeblock}

반복 상태를 확인하려면 다음 요청을 실행하십시오.

요청 예제: 

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

출력
예제: 

```
{
   "count":1,
   "resources":[
      {
         "metadata":{
      "guid":"4091f245-0f0b-42c6-aec9-6ab68185c47f",
            "url":"https://ibm-watson-ml-dev.stage1.mybluemix.net/v3/wml_instances/87452a37-6a8f-4d59-bf88-59c66b5463e4/published_models/9894c3d5-e923-4544-9a7c-2fdb3e4d0908/learning_iterations/4091f245-0f0b-42c6-aec9-6ab68185c47f",
            "created_at":"2017-07-07T11:18:46.742Z",
            "modified_at":"2017-07-07T11:18:48.100Z"
         },
   "entity":{
      "stage":"StartingKernel",
            "published_model":{
               "url":"https://ibm-watson-ml-dev.stage1.mybluemix.net/v3/wml_instances/87452a37-6a8f-4d59-bf88-59c66b5463e4/published_models/9894c3d5-e923-4544-9a7c-2fdb3e4d0908",
               "guid":"9894c3d5-e923-4544-9a7c-2fdb3e4d0908"
            },
            "status":"RUNNING",
            "kernel_id":"db56fc3b-a200-4455-aa70-392aa8ae98b3",
            "spark_service":{
               "credentials":{
            "tenant_id":"s702-faa29053b44952-01f17dcd4c8c",
                  "cluster_master_url":"https://spark.stage1.bluemix.net",
                  "tenant_id_full":"81d716eb-3c8c-40ef-9702-faa29053b449_a2485898-8ed5-43df-8352-01f17dcd4c8c",
                  "tenant_secret":"9f18945c-8e4b-4d2b-8104-f429b27a896d",
                  "instance_id":"81d716eb-3c8c-40ef-9702-faa29053b449",
                  "plan":"ibm.SparkService.PayGoPersonal"
               },
               "version":"2.0"
            }
         }
      },
   ]
}
```
{: codeblock}

다음 요청을 실행하여 평가 메트릭 및 값 목록도 가져올 수 있습니다.

요청 예제: 

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/evaluation_metrics
```
{: codeblock}

출력
예제: 

```
{
  "count": 1,
  "resources": [
    {
      "phase": "training",
      "values": [
        {
          "name": "areaUnderROC",
          "value": 0.94,
          "threshold": 0.8
        }
      ],
      "timestamp": "2017-08-08T10:11:12.000Z",
      "artifactVersionHref": "https://ibm-watson-ml.mybluemix.net/v3/artifacts/models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d/versions/8dfe9548-57ec-4768-8d3e-6c1e7e5cdfc3"
    }
  ]
}
```
{: codeblock}
