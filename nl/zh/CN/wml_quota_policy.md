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

# 配额策略

IBM Watson Machine Learning Engine 按实例强制实施配额，以确保相应的资源分配和使用量。这些策略因帐户概要文件、历史服务使用情况和资源可用性而异。配额策略描述了定价套餐未定义的限制**，可随时更改而不另行通知**。 

当前有效的服务配额限制如下。

## 资源使用情况

资源限制为以下最大值：

-  **最大已发布的模型数**：200（免费套餐），1000（标准和专业套餐）
-  **最大 Spark ML 模型大小**：200 MB
-  **最大已部署的模型数**：1000（标准和专业套餐）

**注**：要了解免费套餐限制，请参阅 [Bluemix 目录](https://console.bluemix.net/catalog/)中[免费套餐](https://console.bluemix.net/catalog/services/machine-learning)的描述。

## 服务请求限制

您每分钟可以对特定 API 发出的请求数是有限的。如果应用程序需要更高的限制，那么必须[联系 IBM Bluemix 支持](https://support.ng.bluemix.net/)来增加配额。

## 部署请求

以下限制适用于部署 API 请求：

-  **周期**：60 秒
-  **缺省限制**：10

## 联机预测请求

以下限制适用于[联机预测](pm_service_api_spark_building.html)请求：

-  **周期**：60 秒
-  **缺省限制**：500

## 资源管理请求

以下限制适用于此列表中的组合总请求数：

[令牌](https://watson-ml-api.mybluemix.net/#/Token)：post、get、delete、put 和 patch 请求

[部署](https://watson-ml-api.mybluemix.net/#/Deployments)：post、get、delete、put 和 patch 请求

-  **周期**：60 秒
-  **缺省限制**：100
