---

copyright:
  years: 2016, 2017
lastupdated: "2017-09-07"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Watson Machine Learning 시작하기
{: #WMLgettingstarted}

IBM® Watson™ Machine Learning을 사용하여 예측 분석을 애플리케이션과 통합하십시오. 데이터 과학자는 기계 학습을 사용하여 예측 모델을 개발하는 반면, 개발자는 기계 학습을 사용하여 더 스마트한 의사결정을 내리고 까다로운 문제점을 해결하며 사용자 성과를 개선하는 애플리케이션을 개발합니다.
{: shortdesc}

## 전제조건

Watson Machine Learning을 사용하려면 Bluemix 카탈로그에서 [여기에 서비스 인스턴스](https://console.bluemix.net/catalog/services/ibm-watson-machine-learning/)를 작성해야 합니다.

## 단계

1. [모델 작성 및 저장](pm_custom_models.html).
2. [모델 배치](pm_service_api_spark_online.html).
3. 애플리케이션에 배치된 모델 `scoring endpoint`를 사용하여 [예측 가져오기](pm_service_api_spark_building.html).

## 정보

Watson Machine Learning 서비스는 프로그래밍 언어에서 호출할 수 있는
REST API 세트입니다. 

Watson Machine Learning 서비스의 초점은
배치에 있지만, 모델 및 파이프라인 작성 및 관련 작업에는 IBM SPSS Modeler 또는
Data Science Experience가 필요하다는 점을 참고하십시오. SPSS Modeler 및 Data Science Experience(Spark MLlib 및 Python scikit-learn 활용)는 모두 기계 학습, 인공 지능 및 통계에서 가져온 다양한 모델링 메소드를 제공합니다. 

## 관련 링크

시작할 준비가 되셨습니까? 서비스의 인스턴스를 작성하거나 애플리케이션을
바인드하려면 [Spark 및 Python 모델과 함께 서비스 사용](using_pm_service_dsx.html) 또는
[SPSS 모델과 함께 서비스 사용](using_pm_service.html)을 참조하십시오.

API 탐색에 관심이 있으면 [Spark 및 Python 모델용 서비스 API](pm_service_api_spark.html) 또는 [SPSS 모델용
서비스 API](pm_service_api_spss.html)를 참조하십시오.

SPSS Modeler 및 여기서 제공하는 모델링 알고리즘에 대한 세부사항은
[IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7)를 참조하십시오. 

IBM Data Science Experience 및 여기서 제공하는 모델링 알고리즘에 대한 세부사항은 [https://datascience.ibm.com](https://datascience.ibm.com)을 참조하십시오. 
