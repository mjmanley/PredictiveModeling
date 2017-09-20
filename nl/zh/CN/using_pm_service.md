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

# 使用服务

SPSS Modeler 建模选用板上提供的这些建模方法支持从数据派生新信息和开发预测模型。每种方法各有所长，最适合于解决特定类型的问题。
{: .shortdesc}

有关 SPSS Modeler 及其提供的建模算法的详细信息，请参阅 [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7)。

在 Bluemix 应用程序和 SPSS Modeler 评分分支设计的输入和输出需求得到实现后，数据分析人员可以更改评分分支的任何内部方面。数据分析人员甚至可以更改刷新操作中使用的模型算法，以确保您能够优化预测性分析，而无需重写应用程序。


## 将服务与 Bluemix 应用程序绑定的步骤
要创建 Bluemix 应用程序并将其绑定到 Machine Learning 服务，请完成以下步骤。

1. 从 [github 存储库](https://github.com/pmservice/customer-satisfaction-prediction)下载 Node.js 样本应用程序代码。

2. 使用 cf create-service 命令创建服务实例：

   ```
   cf create-service pm-20 Free {local naming}
   ```
   {: codeblock}

   例如：

   ```
   cf create-service pm-20 Free my_pm_free
   ```
   {: codeblock}

   此命令将使用名为 my_pm_free 的免费套餐在 Bluemix 空间中创建一个 Machine Learning 服务实例。

3. 使用 `cf create-service-key` 命令创建服务凭证：

   ```
   cf create-service-key "{service instance name}" {vcap key name}
   ```
   {: codeblock}

   例如：

   ```
   cf create-service-key "IBM Watson Machine Learning - my instance" Credentials-1
   ```
   {: codeblock}

   此命令创建 Machine Learning 服务凭证。

4. 使用 cf bind-service 命令将服务实例 my_pm_free 绑定到应用程序。

   ```
   cf bind-service AppName my_pm_service
   ```
   {: codeblock}

   例如：

   ```
   cf bind-service my_app1 my_pm_free
   ```
   {: codeblock}

      此命令将 Machine Learning 服务实例 `my_pm_free` 绑定到 Bluemix 应用程序 my_app1。



5. Machine Learning 凭证：

   在您将 Machine Learning 服务实例绑定到 Bluemix 应用程序后，系统会将 Machine Learning 凭证添加到 `VCAP_SERVICES` 环境变量中：

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

   `VCAP_SERVICES` 环境变量包含以下信息：

   <dl>

   <dt>plan</dt>
   <dd>服务供应中使用的 Machine Learning 套餐。</dd>

   <dt>url</dt>
   <dd>Machine Learning 服务实例的地址。</dd>

   <dt>access_key</dt>
   <dd>要在对此服务实例的所有请求中传递的查询参数 accessKey。</dd>

   </dl>

例如：             

```
Get https://ibm-watson-ml.mybluemix.net/pm/v1/model/sales_model2?accesskey=XXXXXXXXXXXXX
```
{: codeblock}

   以下示例 Node.js 代码显示如何从 `VCAP_SERVICES` 环境变量获取 accessKey：

```
if (process.env.VCAP_SERVICES) {
var env = JSON.parse(process.env.VCAP_SERVICES);
        var credentials = env['pm-20'][0].credentials;
        var accessKey = credentials.access_key;
    }
```
{: codeblock}
