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

# 部署批处理模型 <span class='tag--beta'>Beta</span>

**注**：此功能目前在 Beta 中提供，且仅可用于使用 Spark MLlib。如果您想要参与，请将您自己加入等待列表！
有关更多信息，请参阅：[https://www.ibm.biz/mlwaitlist](https://www.ibm.biz/mlwaitlist)。

**场景名称**：客户满意度预测。

**场景描述**：一家通信公司希望了解哪些客户有流失风险。
展示的模型预测客户流失率。为此，数据研究员开发了一个预测模型并将其与您（开发者）共享。您的任务是部署模型，并通过对已部署的模型发出评分请求来生成预测性分析。

## 使用样本模型

1.  转至 IBM® Watson™ Machine Learning“仪表板”的“样本”选项卡。

2.  在“样本模型”部分中，找到“客户满意度预测”磁贴，并单击“添加模型”按钮 (+)。

现在，您将在“模型”选项卡上的可用模型列表中看到“客户满意度预测”模型。

## 使用 Object Storage 创建批量部署

1.  转至 IBM® Watson™ Machine Learning“仪表板”的“模型”选项卡。

2.  从**操作**菜单中，单击**创建部署**。

3.  在“创建部署”表单中，提供“名称”、“描述”和“批量类型”。

4.  必须提供以下输入：

    **输入连接**：Object Storage 详细信息，将用作模型输入（要评分的客户数据），以及模型输出的存储（在本例中为 results.csv，此文件会自动创建）。

    ```
       {
          "source":{
"fileformat":"csv",
      "firstlineheader":"true",
      "container":"batchjob",
      "inferschema":"1",
      "filename":"TelcoCustomerData.csv",
      "type":"bluemixobjectstorage"
   },
          "connection":{
             "projectid":"252341ed707d4558b5b2da245e785cd7",
             "userid":"b2d83cf6056e040ddb91ca00a2686c7d3",
             "region":"dallas",
             "authurl":"https://identity.open.softlayer.com",
             "password":"eJ_y9R^OE{j?8Ub!!"
          }
       }
    ```
    {: codeblock}

    **输出连接**

    ```
       {
          "target":{
"fileformat":"csv",
      "firstlineheader":"true",
      "container":"batchjob",
      "inferschema":"1",
      "filename":"result.csv",
      "type":"bluemixobjectstorage"
   },
          "connection":{
             "projectid":"252341ed707d4558b5b2da245e785cd7",
             "userid":"b2d83cf6056e040ddb91ca00a2686c7d3",
             "region":"dallas",
             "authurl":"https://identity.open.softlayer.com",
             "password":"eJ_y9R^OE{j?8Ub!!"
          }
       }
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

5.  单击**保存**。

预测结果会保存到 IBM Object Storage 中的 .csv 文件。下面是样本行。

输入文件预览：

```
customerID,gender,SeniorCitizen,Partner,Dependents,tenure,PhoneService,MultipleLines,InternetService,OnlineSecurity,OnlineBackup,DeviceProtection,TechSupport,StreamingTV,StreamingMovies,Contract,PaperlessBilling,PaymentMethod,MonthlyCharges,TotalCharges,Churn
7590-VHVEG,Female,0,Yes,No,1,No,No phone service,DSL,No,Yes,No,No,No,No,Month-to-month,Yes,Electronic check,29.85,29.85,No
5575-GNVDE,Male,0,No,No,34,Yes,No,DSL,Yes,No,Yes,No,No,No,One year,No,Mailed check,56.95,1889.5,No
3668-QPYBK,Male,0,No,No,2,Yes,No,DSL,Yes,Yes,No,No,No,No,Month-to-month,Yes,Mailed check,53.85,108.15,Yes
```
{: codeblock}

输出文件预览：

```
InternetService, Contract, tenure, MonthlyCharges, Churn
Fiber optic, Month-to-month, 2, 70.7, 1
DSL, Two year, 58, 59.9, 0
DSL, Month-to-month, 1, 30.2, 1
DSL, Month-to-month, 17, 64.7, 1
DSL, Month-to-month, 13, 76.2, 0
DSL, Month-to-month, 25, 69.5, 1
Fiber optic, Month-to-month, 8, 80.65, 1
No, One year, 52, 20.4, 0
Fiber optic, Two year, 64, 111.6, 0
Fiber optic, Month-to-month, 1, 79.35, 1
```
{: codeblock}


## 获取部署详细信息

可以检查状态以及与部署的模型相关的参数。

1. 转至 IBM® Watson™ Machine Learning“仪表板”的“部署”选项卡。

2. 从“操作”菜单中选择“查看详细信息”。

## 删除批量部署

如果不再需要该部署，那么可以使用查询将其删除（如以下样本所示）。

1. 转至 IBM® Watson™ Machine Learning“仪表板”的“部署”选项卡。

2. 从“操作”菜单中，选择“删除”。
