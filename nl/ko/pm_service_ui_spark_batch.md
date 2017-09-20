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

# 일괄처리 모델 배치 <span class='tag--beta'>베타</span>

**참고**: 이 기능은 현재 베타이며 Spark MLlib와 함께 사용하기 위한 경우에만 사용 가능합니다. 참여하는 데 관심이 있으면 자신을 대기 목록에 추가하십시오!
자세한 정보는 [https://www.ibm.biz/mlwaitlist](https://www.ibm.biz/mlwaitlist)를 참조하십시오.

**시나리오 이름**: 고객 만족도 예측

**시나리오 설명**: 통신사에서는 어떤 고객이 떠날 위험성이 있는지 알려고 합니다. 제시된 모델은 고객 이탈을 예측합니다. 데이터 과학자는 예측 모델을 개발하고 이를 사용자(개발자)와 공유합니다. 여러분의 태스크는
모델을 배치하고 배치된 모델에 대한 스코어 요청을 작성하여 예측 분석을 생성하는 것입니다. 

## 샘플 모델 사용

1.  IBM® Watson™ Machine Learning 대시보드의 샘플 탭으로 이동하십시오. 

2.  샘플 모델 섹션에서 고객 만족도 예측 타일을 찾아서 모델 추가 단추(+)를 클릭하십시오. 

이제 모델 탭의 사용 가능한 모델 목록에서 샘플 고객 만족도 예측 모델을 보게 됩니다. 

## Object Storage를 사용하여 일괄처리 배치 작성

1.  IBM® Watson™ Machine Learning 대시보드의 모델 탭으로 이동하십시오. 

2.  **조치** 메뉴에서 **배치 작성**을 클릭하십시오.

3.  배치 작성 양식에서 이름, 설명 및 일괄처리 유형을 제공하십시오.

4.  다음 항목을 제공해야 합니다. 

    **입력 연결**: Object Storage 세부사항은 모델에 대한 입력(스코어에 대한 고객 데이터) 및 모델 출력(이 경우 자동으로 작성되는 results.csv)에 대한 스토리지로 사용됩니다. 

    ```
       {
          "source":{
             "fileformat":"csv",
      "firstlineheader":"true",
      "container":"batchjob",
      "inferschema":"1",
      "filename":"TelcoCustomerData.csv",
      "type":"bluemixobjectstorage"
   },
          "connection":{
             "projectid":"252341ed707d4558b5b2da245e785cd7",
             "userid":"b2d83cf6056e040ddb91ca00a2686c7d3",
             "region":"dallas",
             "authurl":"https://identity.open.softlayer.com",
             "password":"eJ_y9R^OE{j?8Ub!!"
          }
       }
    ```
    {: codeblock}

    **출력 연결**

    ```
       {
          "target":{
             "fileformat":"csv",
      "firstlineheader":"true",
      "container":"batchjob",
      "inferschema":"1",
      "filename":"result.csv",
      "type":"bluemixobjectstorage"
   },
          "connection":{
             "projectid":"252341ed707d4558b5b2da245e785cd7",
             "userid":"b2d83cf6056e040ddb91ca00a2686c7d3",
             "region":"dallas",
             "authurl":"https://identity.open.softlayer.com",
             "password":"eJ_y9R^OE{j?8Ub!!"
          }
       }
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

5.  **저장**을 클릭하십시오.

예측 결과가 IBM Object Storage의 .csv 파일에 저장됩니다. 다음은 샘플 행입니다.

입력 파일 미리보기:

```
customerID,gender,SeniorCitizen,Partner,Dependents,tenure,PhoneService,MultipleLines,InternetService,OnlineSecurity,OnlineBackup,DeviceProtection,TechSupport,StreamingTV,StreamingMovies,Contract,PaperlessBilling,PaymentMethod,MonthlyCharges,TotalCharges,Churn
7590-VHVEG,Female,0,Yes,No,1,No,No phone service,DSL,No,Yes,No,No,No,No,Month-to-month,Yes,Electronic check,29.85,29.85,No
5575-GNVDE,Male,0,No,No,34,Yes,No,DSL,Yes,No,Yes,No,No,No,One year,No,Mailed check,56.95,1889.5,No
3668-QPYBK,Male,0,No,No,2,Yes,No,DSL,Yes,Yes,No,No,No,No,Month-to-month,Yes,Mailed check,53.85,108.15,Yes
```
{: codeblock}

출력 파일 미리보기:

```
InternetService, Contract, tenure, MonthlyCharges, Churn
Fiber optic, Month-to-month, 2, 70.7, 1
DSL, Two year, 58, 59.9, 0
DSL, Month-to-month, 1, 30.2, 1
DSL, Month-to-month, 17, 64.7, 1
DSL, Month-to-month, 13, 76.2, 0
DSL, Month-to-month, 25, 69.5, 1
Fiber optic, Month-to-month, 8, 80.65, 1
No, One year, 52, 20.4, 0
Fiber optic, Two year, 64, 111.6, 0
Fiber optic, Month-to-month, 1, 79.35, 1
```
{: codeblock}


## 배치 세부사항 가져오기

배치 모델과 관련된 상태 및 매개변수를 확인할 수 있습니다.

1. IBM® Watson™ Machine Learning Dashboard의 배치 탭으로
   이동하십시오.

2. 조치 메뉴에서 세부사항 보기를 선택하십시오.


## 일괄처리 배치 삭제

배치가 더 이상 필요하지 않은 경우 다음 샘플과 같은 쿼리를 사용하여
배치를 삭제할 수 있습니다.

1. IBM® Watson™ Machine Learning Dashboard의 배치 탭으로
   이동하십시오.

2. 조치 메뉴에서 삭제를 선택하십시오.
