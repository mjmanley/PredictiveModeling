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

# 持續學習系統<span class='tag--beta'>測試版</span>

IBM® Watson™ Machine Learning 持續學習系統提供模型效能的自動監視、重新訓練及重新部署，以確保預測品質。

**情境名稱**：心臟治療的最佳藥物選擇。

**情境說明**：生產心臟藥物的生醫公司想要部署一個選擇心臟治療最佳藥物的模型。當藥物有效性出現新的證明時，應該考慮進行模型更新。資料科學家準備了一套預測模型，並將其與您（開發人員）分享。您的作業是部署模型、設定學習配置，以及反覆執行學習，以評估、重新訓練及重新部署模型。

## 使用範例模型

1. 移至「IBM® Watson™ Machine Learning 儀表板」的「範例」標籤。

2. 在「範例模型」區段中，尋找「心臟藥物選擇」磚，然後按一下「新增模型」按鈕 (+)。

現在您會在模型標籤上看到範例「心臟藥物選擇」模型列在可用的模型清單中。


## 針對已發佈的模型設定持續學習系統

1.  移至「IBM® Watson™ Machine Learning 儀表板」的「模型」標籤。

2.  從**動作**功能表選取**檢視詳細資料**。

3.  向下捲動至**重新訓練詳細資料**，然後按下**編輯**。

4.  您必須提供下列輸入：

    **回饋連線**：Db2 Warehouse on Cloud 詳細資料，這將用來作為模型輸入（回饋資料）以進行模型評估和重新訓練。
    
    ```
    {
        "connection": {
            "username": "dash102204",
            "host": "awh-yp-small02.services.dal.bluemix.net",
            "password": "NweTlYwPY6cu",
            "db": "BLUDB"
        },
        "source": {
            "type": "dashdb",
            "tablename": "DRUG_FEEDBACK_DATA"
        }
    }
    ```
    {: codeblock}

    請使用下列指示，在 Db2 Warehouse on Cloud 中準備 `DRUG_FEEDBACK_DATA` 表格。
    - 建立 [Db2 Warehouse on Cloud 服務](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/)實例（已提供進入方案）。
    - 在 **Db2 Warehouse on Cloud** 中建立 **DRUG_FEEDBACK_DATA** 表格。
      + 從 Git 儲存庫下載 [drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv) 檔案。
      + 按一下**開啟主控台**，以開始使用 **Db2 Warehouse on Cloud** 圖示。
      + 選取**載入資料**及**桌面**載入類型。
      + **拖放**先前下載的檔案，然後按**下一步**。
      + 選取**綱目**以匯入資料，然後按一下**新建表格**。
      + 寫入**新建表格**的名稱，然後按**下一步**以完成資料匯入。
      + 使用 `;` 作為**欄位分隔字元**。
      + 按**下一步**以建立具有上傳資料的表格。

    **附註**：您可以使用此 [REST API 端點](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback)新增回饋記錄至回饋資料庫。

    **資料大小下限**：回饋資料集裡的記錄數下限，以開始模型的評估（學習系統反覆運算的一部分）。

    ```
    20
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

    **臨界值**：將觸發重新訓練程序的臨界值（如果在評估期間計算，度量值低於臨界值）

    ```
    0.8
    ```

    **自動部署重新訓練的模型**：如果重新訓練的模型品質（度量值）比目前已部署的模型好，便部署重新訓練的模型。

5.  按一下**設定**。


## 執行持續學習系統反覆運算

在反覆運算中，將會評估已發佈的模型。如果評估過的正確性低於指定的臨界值，將會觸發模型重新訓練。訓練和回饋兩個資料集都會用於重新訓練與評估。

1. 若要開始新的反覆運算，請從模型**詳細資料**表單，在**監視**標籤上按一下**評估**。

3. 若要檢查反覆運算結果，請前往「評估事件」表格或「圖表」視圖。您可以在那裡找到關於模型品質（根據回饋資料（監視）計算）、重新訓練的模型品質（新模型版本建立並評估）的相關資訊。

4. 若要查看自動訓練模型及其品質的清單，請前往位於「概觀」標籤（模型「檢視詳細資料」->「概觀」）底端的「版本歷程」。
