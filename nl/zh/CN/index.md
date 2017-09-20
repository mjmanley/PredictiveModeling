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

# Watson Machine Learning 入门
{: #WMLgettingstarted}

使用 IBM® Watson™ Machine Learning，可以将预测性分析与您的应用程序相集成。
数据研究员使用机器学习来开发预测模型，而开发人员使用机器学习来创建可进行更智能决策、解决困难问题并改进用户成果的应用程序。
{: shortdesc}

## 先决条件

要在 Bluemix 目录中使用 Watson Machine Learning，必须在此处创建[服务实例](https://console.bluemix.net/catalog/services/ibm-watson-machine-learning/)。

## 步骤

1. [创建和存储模型](pm_custom_models.html)。
2. [部署模型](pm_service_api_spark_online.html)。
3. 使用应用程序中已部署的模型“`评分端点`”来[获取预测](pm_service_api_spark_building.html)。

## 关于

Watson Machine Learning 服务是一组 REST API，可通过任何编程语言进行调用。

Watson Machine Learning 服务的重点是部署，但是请注意，需要 IBM SPSS Modeler 或 Data Science Experience 才能创建并使用模型和管道。SPSS Modeler 和 Data Science Experience（利用 Spark MLlib 和 Python scikit-learn）提供了多种建模方法，它们来源于机器学习、人工智能和统计信息。

## 相关链接

准备好开始了吗？要创建服务的实例或绑定应用程序，请参阅[将服务用于 Spark 和 Python 模型](using_pm_service_dsx.html)或[将服务用于 SPSS 模型](using_pm_service.html)。


如果您想要探索 API，请参阅 [Spark 和 Python 模型的服务 API](pm_service_api_spark.html) 或 [Spark 模型的服务 API](pm_service_api_spss.html)。


有关 SPSS Modeler 及其提供的建模算法的详细信息，请参阅 [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7)。

有关 IBM Data Science Experience 及其提供的建模算法的详细信息，请参阅 [https://datascience.ibm.com](https://datascience.ibm.com)。
