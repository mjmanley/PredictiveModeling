---

copyright:
  years: 2016, 2017
lastupdated: "2017-09-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Continuous learning system <span class='tag--beta'>Beta</span>

The IBM® Watson™ Machine Learning continuous learning system provides automated monitoring of model performance, retraining, and redeployment to ensure prediction quality.

**Scenario name**: Best drug for heart treatment selection.

**Scenario description**: A biomedical company that produces heart drugs wants to deploy a model that selects the best drug for heart treatment. When new evidence emerges on drug effectiveness a model update should be considered. A data scientist prepares a predictive model and shares it with you (the developer). Your task is to deploy the model, set learning configuration, and execute learning iteration to evaluate, retrain, and redeploy the model.

## Using the sample model

1. Go to the Samples tab of the IBM® Watson™ Machine Learning
   Dashboard.

2. In the Sample Models section, find the Heart Drug Selection
   tile and click the Add model button (+).

Now you'll see the sample Heart Drug Selection model in the list of available models on the Models tab.


## Set continuous learning system for published model

1.  Go to the Models tab of the IBM® Watson™ Machine Learning Dashboard.

2.  From the **Actions** menu, click **View Details**.

3.  Scroll down to **Retraining Details** and press **Edit**.

4.  You must provide the following inputs:

    **Feedback Connection**: Db2 Warehouse on Cloud details, which will be used as input (feedback data) for the model evaluation and retraining.
    
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

    Use the following instructions to prepare the  `DRUG_FEEDBACK_DATA` table in Db2 Warehouse on Cloud.
    - Create a [Db2 Warehouse on Cloud Service](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/) instance (an entry plan is offered).
    - Create the **DRUG_FEEDBACK_DATA** table in **Db2 Warehouse on Cloud**.
      + Download  [drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv) file from git repository.
      + Click the **Open the console** to get started with **Db2 Warehouse on Cloud** icon.
      + Select the **Load Data** and **Desktop** load type.
      + **Drag and drop** previously downloaded file and press **Next**.
      + Select **Schema** to import data and click **New Table**.
      + Write name for **new table** than click **Next** to finish data import.
      + Use `;` as **field separator**.
      + Click **Next** to create table with uploaded data.

    **Note**: You can add new feedback records to feedback database using this [REST API endpoint](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback)

    **Minimal Data Size**: The minimal number of records in feedback dataset to start evaluation of the model (part of learning system iteration).

    ```
    20
    ```
    {: codeblock}

    **Spark Connection**: Spark service Credentials can be found on the Service Credentials tab of the Bluemix Spark service dashboard.

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

    **Thresholds**: The threshold value that will trigger retraining process (if calculated during evaluation metric value is below the threshold)

    ```
    0.8
    ```

    **Automatically deploy the retrained model**: Deploy retrained model if it shows better quality (metric value) than currently deployed one.

5.  Click **Set up**.


## Run continuous learning system iteration

Within iteration published model will be evaluated. If the evaluated accuracy is below specified threshold model retraining will be triggered. Both data sets: training and feedback are used for retraining and evaluation.

1. To start a new iteration, from the model **Details** form, on the **Monitor** tab, click **Evaluate**.

3. To check iteration result go either to Evaluation Events table or Chart view. You can find there information about model quality calculated based on feedback data (monitoring), retrained model quality (new model version created and evaluated).

4. To see the list of automatically trained models and their quality go to Version History located at bottom of Overview tab (model View Details -> Overview).
