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

# サービスの使用

Machine Learning サービスに関する以下の重要な情報に注意してください。

## サービスを Bluemix アプリケーションとバインドする手順

Node.js [サンプル・コード](https://github.com/pmservice/product-line-prediction/blob/master/README.md)をダウンロードして、Machine
Learning サービスを試してみることができます。以下のステップを実行して、Bluemix アプリケーションを作成し、Machine Learning サービスをバインドします。これらの例では、一般的なランタイムである Node.js を使用しています。iOS、Ruby、Perl、あるいは Java など他のものも使用できます。


Cloud Foundry ツール (cf) の代わりに Bluemix グラフィカル・インターフェースを使用して、ステップ 1 から 3 までを実行することもできます。

1. `cf create-service` コマンドを使用して、サービス・インスタンスを作成します。


   ```
cf create-service pm-20 Free {local naming}```
   {: codeblock}

   例:

   ```
cf create-service pm-20 Free my_wml_free```
   {: codeblock}

   このコマンドは、Bluemix スペースに `my_wml_free` という名前で、Free プランを使用する 1 つの Machine Learning サービス・インスタンスを作成します。

2. `cf create-service-key` コマンドを使用して、サービス資格情報を作成します。

   ```
cf create-service-key "{service instance name}" {vcap key name}```
   {: codeblock}

   例:

   ```
cf create-service-key "IBM Watson Machine Learning - my instance" Credentials-1```
   {: codeblock}

   このコマンドにより、Machine Learning サービス資格情報が作成されます。

3. cf bind-service コマンドを使用して、サービス・インスタンス `my_wml_free` をアプリケーションにバインドします。

   ```
cf bind-service {AppName} my_wml_free```
   {: codeblock}

   例:

   ```
cf bind-service my_app1 my_wml_free```
   {: codeblock}

   このコマンドは、Machine Learning サービス・インスタンス `my_wml_free` を Bluemix アプリケーション `my_app1` にバインドします。



## Machine Learning の資格情報

Machine Learning サービス・インスタンスを Bluemix アプリケーションにバインドすると、Machine Learning の資格情報が `VCAP_SERVICES` 環境変数に追加されます。

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
           "name": "IBM Watson Machine Learning”
       }
     ]
    }
```
{: codeblock}

   `VCAP_SERVICES` 環境変数には以下の情報が含まれます。


   * `plan` - サービス・プロビジョニングで使用される Machine Learning プラン。
   * `url` - Machine Learning サービス・インスタンスのアドレス。
   * `access_key` - SPSS Modeler ストリームの場合のみ。
   * `instance_id` - Machine Learning インスタンスの固有 ID。
   * `username`、`password` - このサービス・インスタンスへのすべての要求に渡されるアクセス・トークンを生成するために必要となる基本的な許可。例えば、以下のように curl を使用して、アクセス・トークンを生成できます。

要求の例:

```
       curl --basic --user {username}:{password} https://ibm-watson-ml.mybluemix.net/v3/identity/token

       出力例:{"token":"**********"}```
{: codeblock}

   以下の Node.js コードは、`VCAP_SERVICES` 環境変数から username および password を取得する方法の例です。

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
