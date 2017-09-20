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

SPSS Modeler の「モデル作成」パレットにあるモデリング手法を使用して、データから新しい情報を引き出したり、予測モデルを作成したりすることができます。各手法によって、強みや適した問題の種類が異なります。
{: .shortdesc}

SPSS Modeler の概要と提供されるモデリング・アルゴリズムについて詳しくは、[IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7) を参照してください。

お使いの Bluemix アプリケーションや SPSS Modeler スコアリング枝設計の入出力要件が実装されたら、データ・アナリストはスコアリング枝の内部を変更できます。
データ・アナリストは、ユーザーがアプリケーションを書き換えることなく予測分析を微調整できる機能を確保しながら、最新表示操作で使用されるモデル・アルゴリズムまでも変更することができます。



## サービスを Bluemix アプリケーションとバインドする手順
Bluemix アプリケーションを作成し、それを Machine Learning サービスにバインドするには、以下の手順を実行します。

1. [GitHub リポジトリー](https://github.com/pmservice/customer-satisfaction-prediction)から Node.js サンプル・アプリケーション・コードをダウンロードします。

2. cf create-service コマンドを使用して、サービス・インスタンスを作成します。

   ```
   cf create-service pm-20 Free {local naming}
   ```
   {: codeblock}

   例:

   ```
   cf create-service pm-20 Free my_pm_free
   ```
   {: codeblock}

   このコマンドは、Bluemix スペースに my_pm_free という名前で、Free プランを使用する 1 つの Machine Learning サービス・インスタンスを作成します。

3. `cf create-service-key` コマンドを使用して、サービス資格情報を作成します。

   ```
cf create-service-key "{service instance name}" {vcap key name}```
   {: codeblock}

   例:

   ```
cf create-service-key "IBM Watson Machine Learning - my instance" Credentials-1```
   {: codeblock}

   このコマンドにより、Machine Learning サービス資格情報が作成されます。

4. cf bind-service コマンドを使用して、サービス・インスタンス my_pm_free をお使いのアプリケーションにバインドします。

   ```
cf bind-service AppName my_pm_service```
   {: codeblock}

   例:

   ```
cf bind-service my_app1 my_pm_free```
   {: codeblock}

      このコマンドは、Machine Learning サービス・インスタンス
   `my_pm_free` を Bluemix アプリケーション my_app1 にバインドします。



5. Machine Learning の資格情報:

   Machine Learning サービス・インスタンスを Bluemix アプリケーションにバインドすると、Machine Learning の資格情報が `VCAP_SERVICES` 環境変数に追加されます。

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

   `VCAP_SERVICES` 環境変数には以下の情報が含まれます。


   <dl>

   <dt>plan</dt>
   <dd>サービス・プロビジョニングで使用される Machine Learning プラン。</dd>

   <dt>url</dt>
   <dd>Machine Learning サービス・インスタンスのアドレス。</dd>

   <dt>access_key</dt>
   <dd>このサービス・インスタンスへのすべての要求に渡される照会パラメーター accessKey。</dd>

   </dl>

例:             

```
Get https://ibm-watson-ml.mybluemix.net/pm/v1/model/sales_model2?accesskey=XXXXXXXXXXXXX
```
{: codeblock}

   以下は、`VCAP_SERVICES` 環境変数から accessKey を取得する方法を示す Node.js サンプル・コードです。

```
   if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var credentials = env['pm-20'][0].credentials;
        var accessKey = credentials.access_key;
    }
```
{: codeblock}
