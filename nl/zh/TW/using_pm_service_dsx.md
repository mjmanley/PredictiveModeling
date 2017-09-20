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

請注意下列有關 Machine Learning 服務的重要資訊。

## 連結服務與 Bluemix 應用程式的步驟

您可以下載 Node.js [範例程式碼](https://github.com/pmservice/product-line-prediction/blob/master/README.md)，以嘗試 Machine Learning 服務。請完成下列步驟來建立 Bluemix 應用程式及連結 Machine Learning 服務。這些範例使用 Node.js，因為它是熱門的運行環境。可使用其他的運行環境，例如 iOS、Ruby、Perl 或 Java。

請注意，您也可以使用 Bluemix 圖形介面執行步驟 1-3，而不使用 Cloud Foundry 工具 (cf)。

1. 使用 `cf create-service` 指令來建立服務實例：

   ```
   cf create-service pm-20 Free {local naming}
   ```
   {: codeblock}

   例如：

   ```
   cf create-service pm-20 Free my_wml_free
   ```
   {: codeblock}

   這個指令會在 Bluemix 空間建立一個 Machine Learning 服務實例，其中包含名為 `my_wml_free` 的 Free 方案。

2. 使用 `cf create-service-key` 指令來建立服務認證：

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

3. 使用 cf bind-service 指令，將服務實例 `my_wml_free` 連結到應用程式。

   ```
   cf bind-service {AppName} my_wml_free
   ```
   {: codeblock}

   例如：

   ```
   cf bind-service my_app1 my_wml_free
   ```
   {: codeblock}

   這個指令將 Machine Learning 服務實例 `my_wml_free` 連結到 Bluemix 應用程式 `my_app1`。



## Machine Learning 認證

將 Machine Learning 服務實例連結到 Bluemix 應用程式之後， 認證會新增至 `VCAP_SERVICES` 環境變數：

```
    {
     "pm-20-dev": [
       {
         "credentials": {
           "url":
           "https://ibm-watson-ml.mybluemix.net",
           "access_key": "**********",
           "username": "**********",
           "password": "**********",
           "instance_id": "**********"
         },
           "label": "pm-20-dev",
           "plan": "Free",
           "name": "IBM Watson Machine Learning"
       }
     ]
    }
```
{: codeblock}

   `VCAP_SERVICES` 環境變數包括下列資訊：

   * `plan` - 使用於服務供應的 Machine Learning 方案。
   * `url` - Machine Learning 服務實例的位址。
   * `access_key` - 僅限 SPSS Modeler 串流。
   * `instance_id` - Machine Learning 實例唯一 ID。
   * `username`、`password` - 產生存取記號所需的基本授權，它能將所有要求傳入這個服務實例。例如，您可以使用 curl 產生存取記號，如下所示：

要求範例：

```
       curl --basic --user {username}:{password} https://ibm-watson-ml.mybluemix.net/v3/identity/token

       輸出範例：

       {"token":"**********"}
```
{: codeblock}

   下列 Node.js 程式碼是如何從 `VCAP_SERVICES` 環境變數取得 username 和 password 的範例：

```
   if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var credentials = env['pm-20'][0].credentials;
        var username = credentials.username;
        var password = credentials.password;
        var instance_id = credentials.instance_id;
    }
```
{: codeblock}
