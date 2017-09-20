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

# 配額原則

IBM Watson Machine Learning 引擎會對每個實例施行配額，以確保適當的資源配置和使用。這些原則會根據帳戶設定檔、歷程服務用量及資源的可用性而變。配額原則說明定價方案未定義的限制，且**會視情況變更，恕不另行通知**。 

下列服務配額限制目前在作用中。

## 資源用量

資源受限於下列最大值：

-  **已發佈模型上限**：200（免費方案）、1000（標準及專業方案）
-  **Spark ML 模型大小上限**：200 MB
-  **已部署模型上限**：1000（標準及專業方案）

**附註**：若要瞭解免費方案限制，請在 [Bluemix 型錄](https://console.bluemix.net/catalog/)中參閱[免費方案](https://console.bluemix.net/catalog/services/machine-learning)的說明。

## 服務要求限制

您受限於每分鐘可對特定 API 提出的要求數目。如果您的應用程式需要較高的限制，您必須[與 IBM Bluemix 支援中心聯絡](https://support.ng.bluemix.net/)，以增加您的配額。

## 部署要求

下列限制適用於部署 API 要求：

-  **期間**：60 秒
-  **預設限制**：10

## 線上預測要求

下列限制適用於[線上預測](pm_service_api_spark_building.html)要求：

-  **期間**：60 秒
-  **預設限制**：500

## 資源管理要求

下列限制適用於此清單中的結合要求總數：

[記號](https://watson-ml-api.mybluemix.net/#/Token)：post、get、delete、put、patch 要求

[部署](https://watson-ml-api.mybluemix.net/#/Deployments)：post、get、delete、put、patch 要求

-  **期間**：60 秒
-  **預設限制**：100
