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

# 部署串流模型<span class='tag--beta'>測試版</span>

**附註**：此功能目前為測試版，只提供搭配 Spark MLlib 使用。如果您有興趣參與，請將自己新增到等待清單！
如需相關資訊，請參閱：[https://www.ibm.biz/mlwaitlist](https://www.ibm.biz/mlwaitlist)。

**情境名稱**：觀感分析。

**情境說明**：行銷機構想要瞭解有關特定主題的觀感。該機構想要我們開發出一種模型，以將給定的表達方式分類為 POSITIVE 或 NEGATIVE。資料科學家準備預測模型，並與身為開發人員的您分享。您的工作是部署模型，然後對已配置的模型提出評分要求，以產生預測分析模型。

如需相關資訊，請參閱此[文件](https://github.com/pmservice/tweet-sentiment-prediction)。

## 使用範例模型

1. 移至「IBM® Watson™ Machine Learning 儀表板」的「範例」標籤。
2. 在「範例模型」區段中，尋找「觀感預測」磚，然後按一下「新增模型」按鈕 (+)。

現在您會在模型標籤上看到範例「觀感預測」模型列在可用的模型清單中。


## 使用 IBM Message Hub 來建立串流部署

1.  移至「IBM® Watson™ Machine Learning 儀表板」的「模型」標籤。
2.  從「動作」功能表選取「建立部署」。
3.  在「建立部署」表單中提供「名稱」、「說明」及「串流類型」。
4.  您必須提供下列輸入：

    **輸入連線**：IBM Message Hub 主題詳細資料，將會用來做為模型的的輸入（推文），以及模型輸出（預測結果）儲存空間。

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

    **輸出連線**

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

    **Spark 連線**：Spark 服務認證可以在 Bluemix Spark 服務儀表板的「服務認證」標籤上找到。

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

5. 按一下**儲存**。

預測結果會傳送至已定義的 MessageHub 主題（輸出連線）。

## 取得部署詳細資料

您可以檢查與已部署模型相關的狀態和參數。

1. 移至「IBM® Watson™ Machine Learning 儀表板」的「部署」標籤。
2. 從**動作**功能表選取**檢視詳細資料**。

## 刪除串流部署

您可以使用查詢來刪除不再需要的部署，如下列範例所示。

1. 移至「IBM® Watson™ Machine Learning 儀表板」的「部署」標籤。
2. 從「動作」功能表選取「刪除」。
