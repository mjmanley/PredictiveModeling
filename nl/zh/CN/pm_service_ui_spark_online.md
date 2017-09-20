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

# 部署联机模型


**场景名称**：产品系列预测。

**场景描述**：一家卖户外设备的公司想要构建模型，以预测客户对其产品系列的兴趣。
为此，数据研究员准备了一个预测模型并将其与您（开发者）共享。您的任务是部署模型，并通过对已部署的模型发出评分请求来生成客户兴趣预测。

## 使用样本模型

1. 转至 IBM® Watson™ Machine Learning“仪表板”的“样本”选项卡。

2. 在“样本模型”部分中，找到“产品系列预测”磁贴，并单击“添加模型”按钮 (+)。

现在，您将在“模型”选项卡上的可用模型列表中看到样本“产品系列预测”模型。


## 创建联机部署

1. 转至 IBM® Watson™ Machine Learning“仪表板”的“模型”选项卡。

2. 从“操作”菜单中，选择“创建部署”。

3. 在“创建部署”表单中，提供“名称”、“描述”和“联机类型”。

4. 按“保存”按钮。

现在，您将在“部署”选项卡上的可用部署列表中看到联机部署。


## 获取部署详细信息

可以检查状态、评分端点地址 (`Scoring Endpoint`) 以及与部署的模型相关的参数。

1. 转至 IBM® Watson™ Machine Learning“仪表板”的“部署”选项卡。

2. 从“操作”菜单中，选择“查看详细信息”。

请注意，下一步中需要 `Scoring Endpoint` 值来发出评分请求。


## 发出评分请求

评分端点 (`Scoring Endpoint`) 已创建，所以现在可以通过发出评分请求来生成预测。在此场景中，客户记录会传递到预测模型，并返回运动产品预测。

样本记录头：

```
GENDER,AGE,MARITAL_STATUS,PROFESSION
```
{: codeblock}

样本记录：

```
M,27,Single,Professional
F,56,Unspecified,Hospitality
M,45,Married,Retired
```
{: codeblock}

请求示例：

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: Bearer  $token' -d '{"fields": ["GENDER","AGE","MARITAL_STATUS","PROFESSION"],"values": [["M",23,"Single","Student"],["M",55,"Single","Executive"]]}' https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/deployments/{deployment_id}/online
```
{: codeblock}

输出示例：

```
{
   "fields": [
"GENDER",
      "AGE",
      "MARITAL_STATUS",
      "PROFESSION",
      "PROFESSION_IX",
      "GENDER_IX",
      "MARITAL_STATUS_IX",
      "features",
      "rawPrediction",
      "probability",
      "prediction",
      "predictedLabel"
   ],
   "records":[
      [
         "M",
         23,
         "Single",
         "Student",
         6.0,
         0.0,
         1.0,
         [
            0.0,
            23.0,
            1.0,
            6.0
         ],
         [
            5.600716147152702,
            6.482458372136143,
            6.048004170730676,
            0.20929155492307386,
            1.6595297550574055
         ],
         [
            0.2800358073576351,
            0.32412291860680714,
            0.3024002085365338,
            0.010464577746153694,
            0.08297648775287028
         ],
         1.0,
         "Personal Accessories"
      ],
      [
         "M",
         55,
         "Single",
         "Executive",
         3.0,
         0.0,
         1.0,
         [
            0.0,
            55.0,
            1.0,
            3.0
         ],
         [
            6.227653744886563,
            4.325198862164969,
            8.031953760146816,
            1.2319759269281225,
            0.1832177058735289
         ],
         [
            0.3113826872443282,
            0.2162599431082485,
            0.40159768800734086,
            0.06159879634640614,
            0.009160885293676447
         ],
         2.0,
         "Mountaineering Equipment"
      ]
   ]
}
```
{: codeblock}

例如，您可以看到 55 岁的管理人员对 Mountaineering Equipment 感兴趣，而 23 岁的学生则对 Personal Accessories 感兴趣。
