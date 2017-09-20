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

# 継続学習システム (<span class='tag--beta'>ベータ</span>)

継続学習システムは、適切な予測品質を確保するため、モデル・パフォーマンスの自動モニタリング、リトレーニング、および再デプロイメントを提供します。


**シナリオ名**: 最適な心臓治療薬品の選択。

**シナリオの説明**: 心臓用の医薬品を製造するバイオ医薬品会社が、心臓治療のために最適な薬品を選択するモデルをデプロイしたいと考えています。薬品の有効性に関する新しいエビデンスが出現した際にはモデル更新が検討される必要があります。データ・サイエンティストが、予測モデルを準備し、それを開発者と共有します。開発者のタスクは、モデルをデプロイし、learning configuration を設定し、learning iteration を実行して、モデルの評価、リトレーニング、および再デプロイを行うことです。

**注:** サンプルの python [ノートブック](https://apsportal.ibm.com/analytics/notebooks/a97cde0b-5bb8-436a-ae82-83e96adc45e0/view?access_token=6baf4c722e452836f7b505205bc96d9a24b9333ee9b5c39453f6d7751987f798)を試してみることもできます。これは、サンプル・モデルを作成し、学習システムを構成し、最後に learning iteration を実行します。

## サンプル・モデルの使用

1. IBM® Watson™ Machine Learning ダッシュボードの**「サンプル」**タブに移動します。

2. **「サンプル・モデル」**セクションで「Heart Drug Selection」タイルを見つけて、**「モデルの追加」**アイコン (+) をクリックします。

これで、「モデル」タブの使用可能なモデルのリストに、サンプルの「Heart Drug Selection」モデルが表示されるようになります。

## アクセス・トークンの生成

IBM Watson Machine Learning サービス・インスタンスの「サービス資格情報」タブに提供されているユーザーおよびパスワードを使用して、アクセス・トークンを生成します。

要求の例:

```
curl --basic --user <username>:<password> https://ibm-watson-ml.mybluemix.net/v3/identity/token
```
{: codeblock}

出力例:

```
{"token":"**********"}
```
{: codeblock}

以下の端末コマンドを使用して、トークン値を環境変数 token に割り当てます。

```
token="<token_value>"
```
{: codeblock}

## 公開モデルの処理

次のようなインスタンス詳細を取得するには、以下の API 呼び出しを使用します。

* 公開モデルの `url`
* デプロイメントの `url`
* 使用情報

要求の例:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer  $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}
```
{: codeblock}

出力例:

```
{
   "metadata":{
      "guid":"360c510b-012c-4793-ae3f-063410081c3e",
      "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e",
      "created_at":"2017-08-04T09:15:48.344Z",
      "modified_at":"2017-08-22T08:34:47.759Z"
   },
   "entity":{
      "source":"Bluemix",
      "published_models":{
         "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/published_models"
      },
      "usage":{
         "expiration_date":"2017-09-01T00:00:00.000Z",
         "computation_time":{
            "current":4
         },
         "model_count":{
            "limit":1000,
            "current":2
         },
         "prediction_count":{
            "current":16
         },
         "deployment_count":{
            "limit":1000,
            "current":1
         }
      },
      "plan_id":"0f2a3c2c-456b-40f3-9b19-726d2740b11c",
      "status":"Active",
      "organization_guid":"b0e61605-a82e-4f03-9e9f-2767973c084d",
      "region":"us-south",
      "account":{
         "id":"f52968f3dbbe7b0b53e15743d45e5e90",
         "name":"Umit Cakmak's Account",
         "type":"TRIAL"
      },
      "owner":{
         "ibm_id":"31000292EV",
         "email":"umit.cakmak@pl.ibm.com",
         "user_id":"43e0ee0e-6bfb-48fc-bcd8-d61e40d19253",
         "country_code":"POL",
         "beta_user":true
      },
      "deployments":{
         "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/deployments"
      },
      "space_guid":"4c55eb1c-d6fe-4f0a-9390-35c9a7ecf27a",
      "plan":"standard"
   }
}
```
{: codeblock}


**published_models** の `url` が分かったので、次の API 呼び出しを使用してモデルの詳細を取得します。

要求の例:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer  $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models
```
{: codeblock}

出力例:

```
{  
   "count":1,
   "resources":[  
      {  
         "metadata":{
            "guid":"361d0edb-c5c9-4b8c-b353-d968e7dc0b8d",
            "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/published_models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d",
            "created_at":"2017-08-22T08:34:47.597Z",
            "modified_at":"2017-08-22T08:34:47.691Z"
         },
         "entity":{
            "runtime_environment":"spark-2.0",
            "author":{  

            },
            "name":"Best Heart Drug Selection",
            "label_col":"DRUG",
            "training_data_schema":{  
               "fields":[  
                  {  
                     "metadata":{
                        "scale":0,
                        "name":"AGE"
                     },
                     "type":"integer",
                     "name":"AGE",
                     "nullable":true
                  },
                  {  
                     "metadata":{
                        "scale":0,
                        "name":"SEX"
                     },
                     "type":"string",
                     "name":"SEX",
                     "nullable":true
                  },
                  {  
                     "metadata":{
                        "scale":0,
                        "name":"BP"
                     },
                     "type":"string",
                     "name":"BP",
                     "nullable":true
                  },
                  {  
                     "metadata":{
                        "scale":0,
                        "name":"CHOLESTEROL"
                     },
                     "type":"string",
                     "name":"CHOLESTEROL",
                     "nullable":true
                  },
                  {  
                     "metadata":{
                        "scale":6,
                        "name":"NA"
                     },
                     "type":"decimal(12,6)",
                     "name":"NA",
                     "nullable":true
                  },
                  {  
                     "metadata":{
                        "scale":6,
                        "name":"K"
                     },
                     "type":"decimal(13,6)",
                     "name":"K",
                     "nullable":true
                  },
                  {  
                     "metadata":{
                        "scale":0,
                        "name":"DRUG"
                     },
                     "type":"string",
                     "name":"DRUG",
                     "nullable":true
                  }
               ],
               "type":"struct"
            },
            "latest_version":{  
               "url":"https://ibm-watson-ml.mybluemix.net/v2/artifacts/models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d/versions/8dfe9548-57ec-4768-8d3e-6c1e7e5cdfc3",
               "guid":"8dfe9548-57ec-4768-8d3e-6c1e7e5cdfc3",
               "created_at":"2017-08-22T08:34:47.691Z"
            },
            "model_type":"sparkml-model-2.0",
            "deployments":{  
               "count":0,
               "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/published_models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d/deployments"
            },
            "input_data_schema":{  
               "fields":[  
                  {  
                     "metadata":{
                        "scale":0,
                        "name":"AGE"
                     },
                     "type":"integer",
                     "name":"AGE",
                     "nullable":true
                  },
                  {  
                     "metadata":{
                        "scale":0,
                        "name":"SEX"
                     },
                     "type":"string",
                     "name":"SEX",
                     "nullable":true
                  },
                  {  
                     "metadata":{
                        "scale":0,
                        "name":"BP"
                     },
                     "type":"string",
                     "name":"BP",
                     "nullable":true
                  },
                  {  
                     "metadata":{
                        "scale":0,
                        "name":"CHOLESTEROL"
                     },
                     "type":"string",
                     "name":"CHOLESTEROL",
                     "nullable":true
                  },
                  {  
                     "metadata":{
                        "scale":6,
                        "name":"NA"
                     },
                     "type":"decimal(12,6)",
                     "name":"NA",
                     "nullable":true
                  },
                  {  
                     "metadata":{
                        "scale":6,
                        "name":"K"
                     },
                     "type":"decimal(13,6)",
                     "name":"K",
                     "nullable":true
                  }
               ],
               "type":"struct"
            }
         }
      }
}
```
{: codeblock}


## 公開されたモデルの継続学習システムの設定

このサブセクションでは、モデル用に継続学習システムを構成する方法を示します。

### 許可ヘッダーの作成

Watson Machine Learning トークンと Spark インスタンス資格情報を結合する許可ヘッダーを作成するには、以下の詳細を指定します。

*  直前のステップで作成されたアクセス・トークン。
*  Bluemix Spark サービス・ダッシュボードの「サービス資格情報」タブにある Spark サービス資格情報。デプロイメント要求を行う前に、Spark 資格情報が base64 としてエンコードされる必要があります。それらは、要求ヘッダーの X-Spark-Service-Instance フィールドで渡されます。

   使用しているオペレーティング・システムに応じて、以下のいずれかの端末コマンドを発行して base64 エンコードを実行し、それを環境変数に割り当てる必要があります。

   macOS オペレーティング・システムでは、以下のコマンドを使用します。

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64)
   ```
   {: codeblock}

   Microsoft Windows または Linux オペレーティング・システムでは、以下のように `base64` コマンドで `--wrap=0` パラメーターを使用して、base64 エンコードを実行する必要があります。

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64 --wrap=0)
   ```
   {: codeblock}


### フィードバック・データ・セットの作成

学習システムには、トレーニング・データ (モデルのトレーニングで使用されるデータ) およびフィードバック・データ (トレーニングされたモデルを評価するために使用されるデータ) への接続が必要です。以下の説明に従って、**Db2 Warehouse on Cloud** に **DRUG_FEEDBACK_DATA** 表を作成してください。

- [Db2 Warehouse on Cloud サービス](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/)のインスタンスを作成します (入門プランが提供されています)。
- **Db2 Warehouse on Cloud** に **DRUG_FEEDBACK_DATA** 表を作成します。
  + Git リポジトリーから [drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv) ファイルをダウンロードします。
  + **「コンソールを開く」**をクリックし、**「Db2 Warehouse on Cloud」**アイコンで開始します。
  + **「データのロード」**および**「デスクトップ」**ロード・タイプを選択します。
  + 前にダウンロードしたファイルを**ドラッグ・アンド・ドロップ**し、**「次へ」**を押します。
  + データをインポートする**スキーマ**を選択し、**「新規表」**をクリックします。
  + **「新規表」**フィールドに名前を入力し、**「次へ」**をクリックします。
  + **「フィールド分離文字」**にはセミコロン (;) を使用します。
  + **「次へ」**をクリックして、アップロードしたデータで表を作成します。

**注:** この [REST API エンドポイント](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback)を使用して、新規フィードバック・レコードをフィードバック・データベースに追加できます。

### 構成ペイロードの作成

learning configuration を指定するため、以下のエンドポイントを使用する必要があります。

```
https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_configuration
```
   {: codeblock}


ペイロードをファイナライズするため、以下のフィールドの値を定義してください。

* `min_feedback_data_size` - これは、継続学習システムのイテレーションを開始するための、フィードバック・データ・セット内のレコードの最小数です
* `auto_retrain` [never、always、conditionally] - このパラメーターは、リトレーニング・プロセスがトリガーされるタイミングを指定します。[conditionally] は、指定されたしきい値をモデル品質が下回ったらリトレーニング・プロセスをトリガーします。
* `auto_redeploy` [never、always、conditionally] - このパラメーターは、リトレーニングされたモデルがデプロイされるタイミングを指定します。[conditionally] は、新しくトレーニングされたモデルの品質が現在デプロイされているものを上回ったら再デプロイをトリガーします。


要求の例:

```
curl -v -X PUT \
    -H "Content-Type:application/json" \
    -H "Authorization: Bearer $token" \
    -H "X-Spark-Service-Instance: $spark_credentials" \
    -d '{
          "definition": {
            "method": "binary",
            "metrics": [
              {
                "name": "areaUnderROC",
                "threshold": 0.8
              }
            ]
          },
          "feedback_data_ref": {
           "connection": {
            "db": "BLUDB",
            "host": "awh-yp-small02.services.dal.bluemix.net",
            "username": "dash102204",
            "password": "NweTlYwPY6cu"
           },
           "source": {
            "tablename": "DRUG_FEEDBACK_DATA",
            "type": "dashdb"
           }
          },
          "min_feedback_data_size": 100,
          "auto_retrain": "conditionally",
          "auto_redeploy": "conditionally",
          "schedule": {
            "expression": "0/15 * * * * ? *",
            "start": "2017-02-01T10:11:12Z",
            "until": "2017-06-01T10:11:12Z"
          },
          "last_training_record": 0
        }' \
    https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_configuration
```

{: codeblock}

出力例:
```
{
   "min_feedback_data_size":100,
   "auto_retrain":"conditionally",
   "schedule":{
      "expression":"0/15 * * * * ? *",
      "start":"2017-02-01T10:11:12Z",
      "until":"2017-06-01T10:11:12Z"
   },
   "definition":{
      "method":"binary",
      "metrics":[
         {
            "name":"areaUnderROC",
            "threshold":0.8
         }
      ]
   },
   "spark_service":{
      "credentials":{
         "tenant_id":"s971-2eeb9ffe2a3090-35c9a7ecf27a",
         "cluster_master_url":"https://spark.bluemix.net",
         "tenant_id_full":"55f1492d-b385-4fdd-b971-2eeb9ffe2a30_4c55eb1c-d6fe-4f0a-9390-35c9a7ecf27a",
         "tenant_secret":"5e7fc568-e94e-4689-b623-fe62e9ceedd2",
         "instance_id":"55f1492d-b385-4fdd-b971-2eeb9ffe2a30",
         "plan":"ibm.SparkService.PayGoPersonal"
      },
      "version":"2.0"
   },
   "feedback_data_ref":{
      "connection":{
         "db":"BLUDB",
         "host":"awh-yp-small02.services.dal.bluemix.net",
         "username":"dash102204",
         "password":"NweTlYwPY6cu"
      },
      "source":{
         "tablename":"DRUG_FEEDBACK_DATA",
         "type":"dashdb"
      }
   },
   "auto_redeploy":"conditionally"
}
```
{: codeblock}

**注:** この例では、`auto_retrain` パラメーターおよび `auto_redeploy` パラメーターにデフォルト値が使用されています。これらのパラメーターについての詳細は、`learning_configuration` パラメーターの [REST API 資料](http://watson-ml-api.mybluemix.net/#!/Published32Models/put_v3_wml_instances_instance_id_published_models_published_model_id_learning_configuration)に記載されています。

## 継続学習システムのイテレーションの実行

学習システムのイテレーションを開始するには、以下の REST API メソッドを使用します。イテレーション内で、公開されたモデルが評価されます。評価された正確度が指定のしきい値を下回ると、モデルのリトレーニングがトリガーされます。トレーニングとフィードバックの両方のデータ・セットが、リトレーニングおよび評価のために使用されます。

要求の例:

```
curl -X POST --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

出力例:

```
The request has been fulfilled and resulted in a new resource being created.
```
{: codeblock}

イテレーションの状況を確認するには、以下の要求を実行します。

要求の例:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

出力例:

```
{
   "count":1,
   "resources":[
      {
         "metadata":{
            "guid":"4091f245-0f0b-42c6-aec9-6ab68185c47f",
            "url":"https://ibm-watson-ml-dev.stage1.mybluemix.net/v3/wml_instances/87452a37-6a8f-4d59-bf88-59c66b5463e4/published_models/9894c3d5-e923-4544-9a7c-2fdb3e4d0908/learning_iterations/4091f245-0f0b-42c6-aec9-6ab68185c47f",
            "created_at":"2017-07-07T11:18:46.742Z",
            "modified_at":"2017-07-07T11:18:48.100Z"
         },
         "entity":{
            "stage":"StartingKernel",
            "published_model":{
               "url":"https://ibm-watson-ml-dev.stage1.mybluemix.net/v3/wml_instances/87452a37-6a8f-4d59-bf88-59c66b5463e4/published_models/9894c3d5-e923-4544-9a7c-2fdb3e4d0908",
               "guid":"9894c3d5-e923-4544-9a7c-2fdb3e4d0908"
            },
            "status":"RUNNING",
            "kernel_id":"db56fc3b-a200-4455-aa70-392aa8ae98b3",
            "spark_service":{
               "credentials":{
                  "tenant_id":"s702-faa29053b44952-01f17dcd4c8c",
                  "cluster_master_url":"https://spark.stage1.bluemix.net",
                  "tenant_id_full":"81d716eb-3c8c-40ef-9702-faa29053b449_a2485898-8ed5-43df-8352-01f17dcd4c8c",
                  "tenant_secret":"9f18945c-8e4b-4d2b-8104-f429b27a896d",
                  "instance_id":"81d716eb-3c8c-40ef-9702-faa29053b449",
                  "plan":"ibm.SparkService.PayGoPersonal"
               },
               "version":"2.0"
            }
         }
      },
   ]
}
```
{: codeblock}

以下の要求を実行することによって、評価メトリックおよび値のリストを取得することもできます。

要求の例:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/evaluation_metrics
```
{: codeblock}

出力例:

```
{
  "count": 1,
  "resources": [
    {
      "phase": "training",
      "values": [
        {
          "name": "areaUnderROC",
          "value": 0.94,
          "threshold": 0.8
        }
      ],
      "timestamp": "2017-08-08T10:11:12.000Z",
      "artifactVersionHref": "https://ibm-watson-ml.mybluemix.net/v3/artifacts/models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d/versions/8dfe9548-57ec-4768-8d3e-6c1e7e5cdfc3"
    }
  ]
}
```
{: codeblock}
