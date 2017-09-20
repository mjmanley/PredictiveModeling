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

# 服务 API


Machine Learning 服务是可通过任何编程语言调用的一组 REST API，支持将 Data Science Experience 开发的分析集成到应用程序中。将 Bluemix 应用程序绑定到 Machine Learning 服务实例，然后生成预测性分析，您的应用程序需要该分析来为用户提供更高的价值。在[管理仪表板](pm_service_ui_spark.html)中管理模型，并使用该仪表板来创建与应用程序集成的联机、批量或流式部署。

基于通过强大的 [REST API](https://watson-ml-api.mybluemix.net/) 部署在服务实例上的 Data Science Experience 文件（Spark 和 Python 模型）开发应用程序：

*  检索给定预测模型的元数据
*  部署模型和管理已部署的模型
    *  联机部署（评分）
    *  批量部署（支持 Db2 Warehouse on Cloud）
    *  流式部署（支持 IBM MessageHub）
*  检索给定部署的元数据
*  通过对已部署模型发出评分请求来生成预测性分析

请参阅以下部分以获取有关 REST API 用法的示例：

*  [联机部署和评分](pm_service_api_spark_online.html)
*  [使用 Db2 Warehouse on Cloud 批量部署](pm_service_api_spark_batch.html)
*  [使用 MessageHub 流式部署](pm_service_api_spark_streaming.html)
