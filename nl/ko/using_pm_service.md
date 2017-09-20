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

# 서비스 사용

SPSS Modeler 모델링 팔레트에서 사용 가능한 모델링 메소드를 통해
데이터에서 새 정보를 이끌어내고 예측 모델을
개발할 수 있습니다. 각 메소드는 확실한 장점을 포함하고 있으며
특정 유형의 문제점에
가장 적합합니다.
{: .shortdesc}

SPSS Modeler 및 여기서 제공하는 모델링 알고리즘에 대한 세부사항은
[IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7)를 참조하십시오. 

Bluemix 애플리케이션 및 SPSS Modeler 스코어링 분기 디자인이 구현되고 나면
데이터 분석가는 스코어링 분기의 내부 측면을 변경할 수 있습니다. 데이터 분석가는 새로 고치기 오퍼레이션에서 사용되는 모델 알고리즘을
변경할 수도 있으며 애플리케이션을 다시 작성하지 않고 예측 분석을 정밀 조정할 수 있습니다.



## Bluemix 애플리케이션과 서비스를 바인드하는 단계
Bluemix 애플리케이션을 작성하고 Machine Learning 서비스를 바인드하려면 다음 단계를 완료하십시오. 

1. [github 저장소](https://github.com/pmservice/customer-satisfaction-prediction)에서 Node.js 샘플 애플리케이션 코드를 다운로드하십시오.

2. 서비스 인스턴스를 작성하려면 cf create-service 명령을 사용하십시오. 

   ```
   cf create-service pm-20 Free {local naming}
   ```
   {: codeblock}

   예: 

   ```
   cf create-service pm-20 Free my_pm_free
   ```
   {: codeblock}

   이 명령은 Bluemix 영역에서 my_pm_free로 이름 지정된 무료 사용제로
Machine Learning 서비스 인스턴스 한 개를 작성합니다. 

3. 서비스 신임 정보를 작성하려면 `cf create-service-key` 명령을
사용하십시오. 

   ```
   cf create-service-key "{service instance name}" {vcap key name}
   ```
   {: codeblock}

   예: 

   ```
   cf create-service-key "IBM Watson Machine Learning - my instance" Credentials-1
   ```
   {: codeblock}

   이 명령은 Machine Learning 서비스 신임 정보를 작성합니다. 

4. 서비스 인스턴스 my_pm_free를 애플리케이션에 바인드하려면
cf bind-service 명령을 사용하십시오. 

   ```
   cf bind-service AppName my_pm_service
   ```
   {: codeblock}

   예: 

   ```
   cf bind-service my_app1 my_pm_free
   ```
   {: codeblock}

   이 명령은 Machine Learning 서비스 인스턴스
   `my_pm_free`를 Bluemix 애플리케이션 my_app1에 바인드합니다. 

5. Machine Learning 신임 정보:

   Machine Learning 서비스 인스턴스를 Bluemix 애플리케이션에 바인드한 후에
   Machine Learning 신임 정보가 `VCAP_SERVICES` 환경 변수에 추가됩니다.


```
    {   
        "pm-20": {
            "name": "pm20-1",
            "label": "pm-20",
            "plan": "Free",
            "credentials": {
                "url": "https://ibm-watson-ml.mybluemix.net",
                "access_key": "XXXXXXXXXXXXX"
            }
        }       
    }
```
{: codeblock}

   `VCAP_SERVICES` 환경 변수에는 다음 정보가 포함되어 있습니다.


   <dl>

   <dt>plan</dt>
   <dd>서비스 프로비저닝에 사용되는 Machine Learning 플랜입니다. </dd>

   <dt>url</dt>
   <dd>Machine Learning 서비스 인스턴스의 주소입니다. </dd>

   <dt>access_key</dt>
   <dd>모든 요청에서 이 서비스 인스턴스로 전달하는 조회 매개변수 accessKey입니다.
</dd>

   </dl>

예:              

```
Get https://ibm-watson-ml.mybluemix.net/pm/v1/model/sales_model2?accesskey=XXXXXXXXXXXXX
```
{: codeblock}

   `VCAP_SERVICES` 환경 변수에서 accessKey를 얻는 방법을 보여주는 예제 Node.js 코드입니다. 

```
   if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var credentials = env['pm-20'][0].credentials;
        var accessKey = credentials.access_key;
    }
```
{: codeblock}
