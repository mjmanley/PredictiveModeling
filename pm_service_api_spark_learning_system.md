---

copyright:
  years: 2016, 2017
lastupdated: "2017-09-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Continuous learning system <span class='tag--beta'>Beta</span>

Continuous learning system provides automated monitoring of model performance, retraining and redeployment to ensure right predictions quality.


**Scenario name**: Best drug for heart treatment selection.

**Scenario description**: A biomedical company that produces heart drugs
wants to deploy a model that select the best drug for heart treatment. When new evidence emerges on drug effectiveness model update should be considered. A data scientist prepared a predictive model and
shares it with you (the developer). Your task is to deploy the model, set learning configuration and execute learning iteration to evaluate, retrain and redeploy the model.

**Note**: You can also play with sample python  [notebook](https://apsportal.ibm.com/analytics/notebooks/a97cde0b-5bb8-436a-ae82-83e96adc45e0/view?access_token=6baf4c722e452836f7b505205bc96d9a24b9333ee9b5c39453f6d7751987f798) that creates sample model, configures learning system and finally runs learning iteration.

## Using the sample model

1. Go to the **Samples** tab of the IBM® Watson™ Machine Learning Dashboard.

2. In the **Sample Models** section, find the Heart Drug Selection tile and click the **Add model** icon (+).

Now you'll see the sample Heart Drug Selection model in the list of available models on the Models tab.

## Generating the access token

Generate an access token using the user and password available from the Service Credentials tab of the IBM Watson Machine Learning service instance.

Request example:

```
curl --basic --user <username>:<password> https://ibm-watson-ml.mybluemix.net/v3/identity/token
```
{: codeblock}

Output example:

```
{"token":"**********"}
```
{: codeblock}

Use the following terminal command to assign your token value to the environment variable token:

```
token="<token_value>"
```
{: codeblock}

## Working with published models

Use the following API call to get your instance details, such as:

* published models `url`
* deployments `url`
* usage information

Request example:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer  $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}
```
{: codeblock}

Output example:

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


Having **published_models** `url` use the following API call to get model's details:

Request example:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer  $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models
```
{: codeblock}

Output example:

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


## Set continuous learning system for published model

In this subsection you will learn how to configure continuous learning system for your model.

### Prepare Authorization header

To prepare Authorization header that combines Watson Machine Learning token and Spark instance credentials provide the following details:

*  The access token created in the previous step
*  Spark service credentials, which can be found on the Service Credentials tab of the Bluemix Spark service dashboard. Before making the deployment request, Spark credentials must be encoded as base64. They are passed in the header of request in X-Spark-Service-Instance field.

   Depending on the operating system that you are using, you must issue one of the following terminal commands to perform base64 encoding and assign it to the environment variable.

   On the macOS operating system, use the following command:

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64)
   ```
   {: codeblock}

   On the Microsoft Windows or Linux operating systems, you must use the `--wrap=0` parameter with the `base64` command to perform base64 encoding:

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64 --wrap=0)
   ```
   {: codeblock}


### Prepare feedback dataset

Learning System requires connection to training data (data used in model training) as well as feedback data (data that will be used to evaluate trained model). Use below instruction to prepare  **DRUG_FEEDBACK_DATA** table in **Db2 Warehouse on Cloud**.

- Create a [Db2 Warehouse on Cloud Service](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/) instance (an entry plan is offered).
- Create the **DRUG_FEEDBACK_DATA** table in **Db2 Warehouse on Cloud**.
  + Download  [drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv) file from git repository.
  + Click the **Open the console** to get started with **Db2 Warehouse on Cloud** icon.
  + Select the **Load Data** and **Desktop** load type.
  + **Drag and drop** previously downloaded file and press **Next**.
  + Select **Schema** to import data and click **New Table**.
  + In the **new table** field type a name and click **Next**.
  + For the **field separator** use a semicolon (;).
  + Click **Next** to create table with uploaded data.

**Note**: You can add new feedback records to feedback database using this [REST API endpoint](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback)

### Prepare the configuration payload

In order to specify learning configuration, you need to use the following endpoint:

```
https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_configuration
```
   {: codeblock}


Define values of the following fields to finalize payload:

* `min_feedback_data_size` - this is minimal number of records in feedback dataset to start continuous learning system iteration
* `auto_retrain` [never, always, conditionally] - this parameter specifies when retraining process should be triggered. [conditionally] will trigger retraining process when model quality is below specified threshold.
* `auto_redeploy` [never, always, conditionally] - this parameter specifies when retrained model should be deployed. [conditionally] will trigger model redeployment when newly trained model quality is better than currently deployed one.


Request example:

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

Output example:
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

**Note**: In this example we use default values for the `auto_retrain` and `auto_redeploy` parameters. More information about these parameters can be found here in the [REST API documentation](http://watson-ml-api.mybluemix.net/#!/Published32Models/put_v3_wml_instances_instance_id_published_models_published_model_id_learning_configuration) for the `learning_configuration` parameter.

## Run continuous learning system iteration

To start iteration of learning system use REST API method shown below. Within iteration published model will be evaluated. If the evaluated accuracy is below specified threshold model retraining will be triggered. Both data sets: training and feedback are used for retraining and evaluation.

Request example:

```
curl -X POST --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

Output example:

```
The request has been fulfilled and resulted in a new resource being created.
```
{: codeblock}

To check the status of the iteration, issue the following request:

Request example:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

Output example:

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

You can also get the list of evaluation metrics and values by issuing the following request:

Request example:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/evaluation_metrics
```
{: codeblock}

Output example:

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
