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

# 지원되는 기계 학습 프레임워크

IBM Watson Machine Learning 서비스에서는 모델 라이프사이클 관리의 일부로 모델 배치 및 유효성 검증에 사용할 다음 프레임워크를 지원합니다.


## Spark MLlib
Watson Machine Learning Online, Batch(베타), Stream(베타) Deployment 및 Scoring 서비스용 Spark MLlib가 지원됩니다. 특정 버전과 런타임 환경만 지원됩니다.

### 지원되는 버전
*  Spark 2.0

### 제한사항:

  *  분류와 회귀 모델만 지원됩니다.
  *  사용자 정의 변환자, 사용자 정의 함수 및 클래스에 대한 참조를 포함하는 모델은 지원되지 않습니다. 
  * scikit-learn 모델 배치 요청 중에 리턴된 "스키마" 엔드포인트는 이 단계에서 지원되지 않습니다.
  *  Spark 모델의 일괄처리 및 스트림 지원은 베타 상태입니다. 참여하는 데 관심이 있으면 자신을 [대기 목록](https://www.ibm.biz/mlwaitlist)에 추가하십시오.

  * Spark 모델의 연속 학습 시스템은 베타 상태에 있습니다. 참여하는 데 관심이 있으면 자신을 [대기 목록](https://www.ibm.biz/mlwaitlist)에 추가하십시오.


## Scikit-learn
Watson Machine Learning Online Deployment and Scoring 서비스용 scikit-learn이 지원됩니다. 특정 버전과 런타임 환경만 지원됩니다.

### 지원되는 버전

- Anaconda 4.2.x for Python 3.5 런타임
- Scikit-Learn 0.17

### Python 런타임

WML Online Deployment and Scoring 서비스를 사용하여 배치해야 하는 모델의 Python 런타임은 Python 3.5입니다.

Python 2.7 런타임에 모델이 작성된 경우 Python2.7과 Python3.5 사이의 비호환성으로 인해 배치에 실패할 수 있습니다.

### 지원되는 Python 패키지

WML Online Deployment and Scoring 서비스에서 지원하는 Python 패키지 목록은 [여기](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35)에 있습니다.

### 제한사항

다음 제한사항 중 일부 또는 모두를 포함할 수 있는 제한사항이 있습니다.

* 분류 및 회귀 모델만 지원됩니다.
* 모델에는 Anaconda 4.2.x for Python 3.5 런타임에서 지원하는 패키지(및 패키지 버전)에 대한 참조만 포함될 수 있습니다.
* 배치 요청 중에 리턴된 "스키마" 엔드포인트는 구현되지 않습니다.
* 이 단계에서 스코어링 요청에 대한 응답으로 예측 확률이 리턴되지 않습니다.
* "predict()" API에 대한 입력 유형으로 Pandas Dataframe이 필요한 모델은 지원되지 않습니다.
* 사용자 정의 변환자, 사용자 정의 함수 및 클래스에 대한 참조를 포함하는 모델은 지원되지 않습니다. 

## XGBoost <span class='tag--beta'>Beta</span>
Watson Machine Learning Online Deployment and Scoring 서비스용 XGBoost가 지원됩니다. 특정 버전과 런타임 환경만 지원됩니다.

### 지원되는 버전

- XGBoost 0.6
- Anaconda 4.2.x for Python 3.5 런타임
- Scikit-Learn 0.17

### Python 런타임

WML Online Deployment and Scoring 서비스를 사용하여 배치해야 하는 모델의 Python 런타임은 Python 3.5입니다.

Python 2.7 런타임에 모델이 작성된 경우 Python2.7과 Python3.5 사이의 비호환성으로 인해 배치에 실패할 수 있습니다.

### 지원되는 Python 패키지

WML Online Deployment and Scoring 서비스에서 지원하는 Python 패키지 목록은 [여기](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35)에 있습니다.

### 제한사항

다음 제한사항 중 일부 또는 모두를 포함할 수 있는 제한사항이 있습니다.
* 현재 XGBoost 지원은 XGBoost의 Scikit-Learn 랩퍼(즉, xgboost.sklearn.XGBClassifier 및 xgboost.sklearn.XGBRegressor)를 사용하여 작성된 모델에 사용할 수 있습니다.
* 모델에는 Anaconda 4.2.x for Python 3.5 런타임에서 지원하는 패키지(및 패키지 버전)에 대한 참조만 포함될 수 있습니다.
* 배치 요청 중에 리턴된 "스키마" 엔드포인트는 구현되지 않습니다.
* 이 단계에서 스코어링 요청에 대한 응답으로 예측 확률이 리턴되지 않습니다.
* 사용자 정의 변환자, 사용자 정의 함수 및 클래스에 대한 참조를 포함하는 모델은 지원되지 않습니다. 

## SPSS Modeler

Watson Machine Learning Online, Batch Deployment and Scoring 서비스용 XSPSS Modeler 스트림이 지원됩니다. 특정 버전과 런타임 환경만 지원됩니다.

### 지원되는 버전

*  SPSS Modeler 17.1
*  SPSS Modeler 18.0

### 제한사항

SPSS Modeler 스트림의 제한사항은 다음과 같습니다.

*  실시간 스코어링에서 사용할 수 있도록 스코어링 분기를 준비할 때
스코어 요청에서 수신되는 입력 데이터는 스코어링 분기로 디자인된 소스 노드를 대체해야 하며,
최종 예측 분석 결과물은 응답 플로우로 반환되어야 합니다(실제로 스코어링 분기 디자인의 터미널 노드를 대체함). 
*  Bluemix에서 스코어링 분기가 실시간 실행을 위해 준비되어 있으므로 이는 외부 서비스에 대한 연결이 필요하지 않습니다. 
예를 들어, IBM Analytical Decision Management 스코어링 분기 디자인에는
IBM SPSS Collaboration and Deployment Services 저장소에 저장된 규칙이나 모델에 대한 참조가 포함될 수 없습니다. 
*  Bluemix에서 실시간 스코어링에 대한 스코어링 분기의 실행은 외부 서비스를 요구할 수 없습니다. 
예를 들어, 실시간으로 IBM SPSS Analytic Server 및 Apache Hadoop 데이터 저장소가 필요한
모델 알고리즘에 대해 배치하고 스코어링할 수 없습니다. 
*  Machine Learning에서는 Modeler 임베디드 Python 스크립팅을 지원합니다. Machine Learning에서 실행되기 전에 스트림 처리에 사용된 방법으로 인한
몇 가지 제한사항이 있습니다. 일반적으로, 스트림의 실행을 제어하도록 선택한 경우 사용자는 분기의 터미널 노드를 참조합니다. Machine Learning의 경우,
스트림을 처리할 때는 대체될 JSON의 노드를 식별한 후에 스트림이 실행되기 전에 대체를 실행합니다. 
이에 따라 참조된 입력 및 내보내기 노드가 더 이상 존재하지 않으므로 스트림은 스크립트에서 실패합니다. 
솔루션은 다른 노드의 ID를 사용하여 실행 중에 분기를 고유하게 식별하는 것입니다. 
이는 임베디드 Python 스크립트에서 정의된 대로 스트림이 실행되도록 보장합니다. 

## 자세히 보기

IBM SPSS Analytic Server 훈련 예측 모델의 최신 지원에 대한 세부사항은 [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/)의 [SPSS Analytic Server](https://www.ibm.com/support/knowledgecenter/SSWLVY) 섹션을 참조하십시오.
