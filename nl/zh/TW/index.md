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

# 開始使用 Watson Machine Learning
{: #WMLgettingstarted}

使用 IBM® Watson™ Machine Learning 可以整合預測分析與您的應用程式。資料科學家使用機器學習開發預測模型，而開發人員則使用機器學習開發應用程式，做出更聰明的決策、解決困難的問題，以及改善使用者結果。
{: shortdesc}

## 必要條件

若要從 Bluemix 型錄使用 Watson Machine Learning，您必須[在這裡建立服務實例](https://console.bluemix.net/catalog/services/ibm-watson-machine-learning/)。

## 步驟

1. [建立並儲存模型](pm_custom_models.html)。
2. [部署模型](pm_service_api_spark_online.html)。
3. 在應用程式使用已部署的模型 `scoring endpoint`，以[取得預測](pm_service_api_spark_building.html)。

## 關於

Watson Machine Learning 服務是一組 REST API，可以從任何程式設計語言呼叫。

Watson Machine Learning 服務的焦點是部署，但請注意，需要有 IBM SPSS Modeler 或 Data Science Experience，才能編寫及使用模型和管線。SPSS Modeler 和 Data Science Experience（利用 Spark MLlib）提供各種建模方法，這些方法取自機器學習、人工智慧及統計資料。


## 相關鏈結

準備好要開始了嗎？若要建立服務的實例或是連結應用程式，請參閱[使用服務搭配 Spark
及 Python 模型](using_pm_service_dsx.html)或[使用服務搭配 SPSS 模型](using_pm_service.html)。

如果您有興趣探索 API，請參閱 [Spark 及 Python 模型的服務 API](pm_service_api_spark.html) 或 [SPSS 模型的服務 API](pm_service_api_spss.html)。

如需 SPSS Modeler 及其提供之建模演算法的詳細資料，請參閱 [IBM Knowledge
Center](https://www.ibm.com/support/knowledgecenter/SS3RA7)。

如需 IBM Data Science Experience 及其提供之建模演算法的詳細資料，請參閱 [https://datascience.ibm.com](https://datascience.ibm.com)。
