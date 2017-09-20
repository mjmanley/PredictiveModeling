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

# 持续学习系统 <span class='tag--beta'>Beta</span>

持续学习系统可自动监视模型性能、重新培训和重新部署，以确保正确的预测质量。


**场景名称**：选择治疗心脏疾病的最佳药物。

**场景描述**：一家生产心脏疾病药物的生物医学公司希望部署一个模型，用于选择治疗心脏疾病的最佳药物。在药物有效性方面出现新的证据时，应考虑更新模型。为此，数据研究员准备了一个预测模型并将其与您（开发者）共享。您的任务是部署模型，设置学习配置和执行学习迭代来评估、重新培训并重新部署模型。

**注**：您还可以播放样本 Python [配置页](https://apsportal.ibm.com/analytics/notebooks/a97cde0b-5bb8-436a-ae82-83e96adc45e0/view?access_token=6baf4c722e452836f7b505205bc96d9a24b9333ee9b5c39453f6d7751987f798)，此配置页用于创建样本模型，配置学习系统并最终运行学习迭代。

## 使用样本模型

1. 转至 IBM® Watson™ Machine Learning“仪表板”的**样本**选项卡。

2. 在**样本模型**部分中，找到“选择心脏疾病药物”磁贴，并单击**添加模型**图标 (+)。

现在，您将在“模型”选项卡上的可用模型列表中看到样本“选择心脏疾病药物”模型。

## 生成访问令牌

使用 IBM Watson Machine Learning 服务实例的“服务凭证”选项卡上提供的用户和密码来生成访问令牌。

请求示例：

```
curl --basic --user <username>:<password> https://ibm-watson-ml.mybluemix.net/v3/identity/token
```
{: codeblock}

输出示例：

```
{"token":"**********"}
```
{: codeblock}

使用以下终端命令将令牌值分配给环境变量令牌：

```
token="<token_value>"
```
{: codeblock}

## 处理已发布的模型

使用以下 API 调用来获取实例详细信息，例如：

* published models `url`
* deployments `url`
* usage information

请求示例：

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}
```
{: codeblock}

输出示例：

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


具有 **published_models** `url` 时，请使用以下 API 调用来获取模型的详细信息：

请求示例：

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer  $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models
```
{: codeblock}

输出示例：

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


## 为已发布的模型设置持续学习系统

在此子部分中，您将了解如何为模型配置持续学习系统。

### 准备 Authorization 头

要准备用于将 Watson Machine Learning 令牌与 Spark 实例凭证组合在一起的 Authorization 头，请提供以下详细信息：

*  在上一步中创建的访问令牌
*  Spark 服务凭证，可在 Bluemix Spark 服务仪表板的“服务凭证”选项卡上找到。在发出部署请求之前，必须将 Spark 凭证编码为基本 64 位。它们将在请求头中的 X-Spark-Service-Instance 字段中传递。

   根据所使用的操作系统，必须发出以下某个终端命令来执行基本 64 位编码，并将其分配给环境变量。

   在 macOS 操作系统上，使用以下命令：

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64)
   ```
   {: codeblock}

   在 Microsoft Windows 或 Linux 操作系统上，必须将 `--wrap=0` 参数用于 `base64` 命令来执行基本 64 位编码：

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64 --wrap=0)
   ```
   {: codeblock}


### 准备反馈数据集

学习系统需要连接到培训数据（模型培训中使用的数据）以及反馈数据（将用于评估经过培训的模型的数据）。使用以下指示信息在 **Db2 Warehouse on Cloud** 中准备 **DRUG_FEEDBACK_DATA** 表。

- 创建 [Db2 Warehouse on Cloud Service](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/) 实例（提供了入门套餐）。
- 在 **Db2 Warehouse on Cloud** 中创建 **DRUG_FEEDBACK_DATA** 表。
  + 从 Git 存储库下载 [drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv) 文件。
  + 单击**打开控制台**以开始使用 **Db2 Warehouse on Cloud** 图标。
  + 选择**装入数据**和**桌面**装入类型。
  + **拖放**先前下载的文件，然后按**下一步**。
  + 选择**模式**以导入数据，然后单击**新建表**。
  + 在**新表**字段中，输入名称，然后单击**下一步**。
  + 对于**字段分隔符**，请使用分号 (;)。
  + 单击**下一步**，以使用上传的数据来创建表。

**注**：您可以使用此 [REST API 端点](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback)向反馈数据库添加新的反馈记录。

### 准备配置有效内容

为了指定学习配置，您需要使用以下端点：

```
https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_configuration
```
   {: codeblock}


定义以下字段的值以最终完成有效内容：

* `min_feedback_data_size` - 这是可开始持续学习系统迭代所需的反馈数据集内的最小记录数
* `auto_retrain` [never、always 和 conditionally] - 此参数指定何时应该触发重新培训过程。[conditionally] 将在模型质量低于指定阈值时，触发重新培训过程。
* `auto_redeploy` [never、always 和 conditionally] - 此参数指定何时应该部署经过重新培训的模型。[conditionally] 将在新培训的模型的质量比当前部署的模型的质量更好时，触发模型重新部署。


请求示例：

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
           "connection":{
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

输出示例：
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
            "name": "areaUnderROC",
        "threshold": 0.8
      }
    ]
   },
      "spark_service":{
         "credentials": {
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

**注**：在此示例中，使用的是 `auto_retrain` 和 `auto_redeploy` 参数的缺省值。有关这些参数的更多信息位于 `learning_configuration` 参数的 [REST API 文档](http://watson-ml-api.mybluemix.net/#!/Published32Models/put_v3_wml_instances_instance_id_published_models_published_model_id_learning_configuration)中。

## 运行持续学习系统迭代

要启动学习系统迭代，请使用下面显示的 REST API 方法。在迭代期间，将对已发布的模型进行评估。如果评估后的准确性低于指定的阈值，那么将触发模型重新培训。培训和反馈这两个数据集将用于重新培训和评估。

请求示例：

```
curl -X POST --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

输出示例：

```
该请求已执行，并导致创建了新资源。
```
{: codeblock}

要检查迭代的状态，请发出以下请求：

请求示例：

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

输出示例：

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
               "credentials": {
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

您还可以通过发出以下请求来获取评估度量及其值的列表：

请求示例：

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/evaluation_metrics
```
{: codeblock}

输出示例：

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
