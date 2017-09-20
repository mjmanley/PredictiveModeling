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

# 스트리밍 모델 배치 <span class='tag--beta'>베타</span>

**참고**: 이 기능은 현재 베타이며 Spark MLlib와 함께 사용하기 위한 경우에만 사용 가능합니다. 참여하는 데 관심이 있으면 자신을 대기 목록에 추가하십시오!
자세한 정보는 [https://www.ibm.biz/mlwaitlist](https://www.ibm.biz/mlwaitlist)를 참조하십시오.

**시나리오 이름**: 감성 분석

**시나리오 설명**: 마케팅 에이전시에서 특정 주제에 대한 감성에 대해 알고자 합니다.
에이전시는 POSITIVE 또는 NEGATIVE와 같은 주어진 명령문을 분류하는 모델을
개발하도록 요청합니다. 데이터 과학자는 예측 모델을 준비하고
사용자(개발자)와 이를 공유합니다. 여러분의 태스크는
모델을 배치하고 배치된 모델에 대한 스코어 요청을 작성하여 예측 분석을 생성하는 것입니다. 

자세한 정보는 이 [문서](https://github.com/pmservice/tweet-sentiment-prediction)를 참조하십시오.

## 샘플 모델 사용

1. IBM® Watson™ Machine Learning 대시보드의 샘플 탭으로 이동하십시오. 
2. 샘플 모델 섹션에서 감성 예측 타일을 찾아서 모델 추가 단추(+)를 클릭하십시오. 

이제 모델 탭의 사용 가능한 모델 목록에 샘플 감성 예측 모델이 표시됩니다. 


## IBM Message Hub를 사용하여 스트리밍 배치 작성

1.  IBM® Watson™ Machine Learning 대시보드의 모델 탭으로 이동하십시오. 
2.  조치 메뉴에서 배치 작성을 선택하십시오.
3.  배치 작성 양식에서 이름, 설명 및 스트림 유형을 제공하십시오.
4.  다음 항목을 제공해야 합니다. 

    **입력 연결**: 모델에 대한 입력(트윗) 및 모델 출력(예측 결과)에 대한 스토리지로 사용되는 IBM Message Hub 주제 세부사항입니다.

    ```
  {
     "connection":{
      "kafka_brokers_sasl":[
         "kafka01-prod01.messagehub.services.us-south.bluemix.net:9093",
         "kafka02-prod01.messagehub.services.us-south.bluemix.net:9093",
         "kafka03-prod01.messagehub.services.us-south.bluemix.net:9093",
         "kafka04-prod01.messagehub.services.us-south.bluemix.net:9093",
         "kafka05-prod01.messagehub.services.us-south.bluemix.net:9093"
      ],
      "kafka_admin_url":"https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443",
      "api_key":"Dv5kEVNNsbuJ9RFEKdUhIn2hruipIrsBolge6v1uQmTzEQti",
      "mqlight_lookup_url":"https://mqlight-lookup-prod01.messagehub.services.us-south.bluemix.net/Lookup?serviceId=5448397d-cb22-4698-8a2b-ffb04f43a4cb",
      "kafka_rest_url":"https://kafka-rest-prod01.messagehub.services.us-south.bluemix.net:443",
      "user":"Dv5kEVNNsbuJ9RFE",
      "password":"KdahIn2hruipIrsBolge6v1uQmTzEQti"
   },
   "source":{
      "topic":"sinput",
         "type":"kafka"
      }
   }
    ```
    {: codeblock}

    **출력 연결**

    ```
 {
    "connection":{
       "kafka_brokers_sasl":[
          "kafka01-prod01.messagehub.services.us-south.bluemix.net:9093",
          "kafka02-prod01.messagehub.services.us-south.bluemix.net:9093",
          "kafka03-prod01.messagehub.services.us-south.bluemix.net:9093",
          "kafka04-prod01.messagehub.services.us-south.bluemix.net:9093",
          "kafka05-prod01.messagehub.services.us-south.bluemix.net:9093"
       ],
       "kafka_admin_url":"https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443",
       "api_key":"Dv5kEVNNsbuJ9RFEKdUhIn2hruipIrsBolge6v1uQmTzEQti",
       "mqlight_lookup_url":"https://mqlight-lookup-prod01.messagehub.services.us-south.bluemix.net/Lookup?serviceId=5448397d-cb22-4698-8a2b-ffb04f43a4cb",
       "kafka_rest_url":"https://kafka-rest-prod01.messagehub.services.us-south.bluemix.net:443",
       "user":"Dv5kEVNNsbuJ9RFE",
       "password":"KdahIn2hruipIrsBolge6v1uQmTzEQti"
    },
    "target":{
       "topic":"soutput",
       "type":"kafka"
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

5. **저장**을 클릭하십시오.

정의된 MessageHub 주제에 예측 결과가 전송됩니다(출력 연결).

## 배치 세부사항 가져오기

배치 모델과 관련된 상태 및 매개변수를 확인할 수 있습니다.

1. IBM® Watson™ Machine Learning Dashboard의 배치 탭으로
   이동하십시오.
2. **조치** 메뉴에서 **세부사항 보기**를 클릭하십시오.

## 스트리밍 배치 삭제

배치가 더 이상 필요하지 않은 경우 다음 샘플과 같은 쿼리를 사용하여
배치를 삭제할 수 있습니다.

1. IBM® Watson™ Machine Learning Dashboard의 배치 탭으로
   이동하십시오.

2. 조치 메뉴에서 삭제를 선택하십시오.
