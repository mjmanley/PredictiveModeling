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

# 使用此服務

SPSS Modeler 建模選用區上的可用建模方法可讓您從資料中衍生新資訊，以及開發預測模型。每一個方法有特定強度，最適合特定類型的問題。
{: .shortdesc}

如需 SPSS Modeler 及其提供之建模演算法的詳細資料，請參閱 [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7)。

在實作 Bluemix 應用程式及 SPSS Modeler 評分分支設計的輸入及輸出需求之後，「資料分析師」可以變更評分分支的任何內部層面。「資料分析師」甚至可以變更某個重新整理作業中使用的模型演算法，確保您有能力細部調整預測分析，而不需要重寫應用程式。


## 連結服務與 Bluemix 應用程式的步驟
請完成下列步驟來建立 Bluemix 應用程式並將它連結至 Machine Learning 服務。

1. 從 [github 儲存庫](https://github.com/pmservice/customer-satisfaction-prediction)下載 Node.js 範例應用程式碼。

2. 使用 cf create-service 指令來建立服務實例：

   ```
   cf create-service pm-20 Free {local naming}
   ```
   {: codeblock}

   例如：

   ```
   cf create-service pm-20 Free my_pm_free
   ```
   {: codeblock}

   這個指令會在 Bluemix 空間建立一個 Machine Learning 服務實例，其中包含名為 my_pm_free 的 Free 方案。

3. 使用 `cf create-service-key` 指令來建立服務認證：

   ```
   cf create-service-key "{service instance name}" {vcap key name}
   ```
   {: codeblock}

   例如：

   ```
   cf create-service-key "IBM Watson Machine Learning - my instance" Credentials-1
   ```
   {: codeblock}

   這個指令會建立 Machine Learning 服務認證。

4. 使用 cf bind-service 指令，將服務實例 my_pm_free 連結到應用程式。

   ```
   cf bind-service AppName my_pm_service
   ```
   {: codeblock}

   例如：

   ```
   cf bind-service my_app1 my_pm_free
   ```
   {: codeblock}

   這個指令將 Machine Learning 服務實例 `my_pm_free` 連結到 Bluemix 應用程式 my_app1。

5. Machine Learning 認證：

   將 Machine Learning 服務實例連結到 Bluemix 應用程式之後， 認證會新增至 `VCAP_SERVICES` 環境變數：

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

   `VCAP_SERVICES` 環境變數包括下列資訊：

   <dl>

   <dt>plan</dt>
   <dd>使用於服務供應的 Machine Learning 方案。</dd>

   <dt>url</dt>
   <dd>Machine Learning 服務實例的位址。</dd>

   <dt>access_key</dt>
   <dd>查詢參數 accessKey，它能將所有要求傳入這個服務實例。</dd>

   </dl>

例如：             

```
Get https://ibm-watson-ml.mybluemix.net/pm/v1/model/sales_model2?accesskey=XXXXXXXXXXXXX
```
{: codeblock}

   下列範例 Node.js 程式碼顯示如何從 `VCAP_SERVICES` 環境變數取得 accessKey：

```
   if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var credentials = env['pm-20'][0].credentials;
        var accessKey = credentials.access_key;
    }
```
{: codeblock}
