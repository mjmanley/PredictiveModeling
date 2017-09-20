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

IBM® Watson™ Machine Learning 持续学习系统可自动监视模型性能、重新培训和重新部署，以确保预测质量。

**场景名称**：选择治疗心脏疾病的最佳药物。

**场景描述**：一家生产心脏疾病药物的生物医学公司希望部署一个模型，用于选择治疗心脏疾病的最佳药物。在药物有效性方面出现新的证据时，应考虑更新模型。为此，数据研究员准备了一个预测模型并将其与您（开发者）共享。您的任务是部署模型，设置学习配置和执行学习迭代来评估、重新培训并重新部署模型。

## 使用样本模型

1. 转至 IBM® Watson™ Machine Learning“仪表板”的“样本”选项卡。

2. 在“样本模型”部分中，找到“选择心脏疾病药物”磁贴，并单击“添加模型”按钮 (+)。

现在，您将在“模型”选项卡上的可用模型列表中看到样本“选择心脏疾病药物”模型。


## 为已发布的模型设置持续学习系统

1.  转至 IBM® Watson™ Machine Learning“仪表板”的“模型”选项卡。

2.  从**操作**菜单中，单击**查看详细信息**。

3.  向下滚动到**重新培训详细信息**，然后按**编辑**。

4.  必须提供以下输入：

    **反馈连接**: Db2 Warehouse on Cloud 详细信息，这些信息将用作模型评估和重新培训的输入（反馈数据）。
    
    ```
    {
        "connection":{
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

    使用以下指示信息在 Db2 Warehouse on Cloud 中准备 `DRUG_FEEDBACK_DATA` 表。
    - 创建 [Db2 Warehouse on Cloud Service](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/) 实例（提供了入门套餐）。
    - 在 **Db2 Warehouse on Cloud** 中创建 **DRUG_FEEDBACK_DATA** 表。
      + 从 Git 存储库下载 [drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv) 文件。
      + 单击**打开控制台**以开始使用 **Db2 Warehouse on Cloud** 图标。
      + 选择**装入数据**和**桌面**装入类型。
      + **拖放**先前下载的文件，然后按**下一步**。
      + 选择**模式**以导入数据，然后单击**新建表**。
      + 为**新表**编写名称，然后单击**下一步**以完成数据导入。
      + 将 `;` 用作**字段分隔符**。
      + 单击**下一步**，以使用上传的数据来创建表。

    **注**：您可以使用此 [REST API 端点](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback)向反馈数据库添加新的反馈记录。

    **最小数据大小**：可开始评估模型所需的反馈数据集内的最小记录数（是学习系统迭代的一部分）。

    ```
    20
    ```
    {: codeblock}

    **Spark 连接**：Spark 服务凭证位于 Bluemix Spark 服务仪表板的“服务凭证”选项卡上。

    ```
{
    "credentials": {
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

    **阈值**：将触发重新培训过程的阈值（如果在评估度量值期间计算出的值低于阈值）

    ```
    0.8
    ```

    **自动部署经过重新培训的模型**：如果经过重新培训的模型表现出的质量（度量值）比当前部署的更好，那么会部署经过重新培训的模型。
5.  单击**设置**。


## 运行持续学习系统迭代

在迭代期间，将对已发布的模型进行评估。如果评估后的准确性低于指定的阈值，那么将触发模型重新培训。培训和反馈这两个数据集将用于重新培训和评估。

1. 要启动新的迭代，请在模型的**详细信息**表单中的**监视**选项卡上，单击**评估**。

3. 要检查迭代结果，请转至“评估事件”表或“图表”视图。在其中可以找到有关根据反馈数据（监视）计算的模型质量和经过重新培训的模型的质量（创建和评估的新模型版本）的信息。

4. 要查看自动培训的模型及其质量的列表，请转至“概述”选项卡（模型的“查看详细信息”->“概述”）底部的“版本历史记录”。
