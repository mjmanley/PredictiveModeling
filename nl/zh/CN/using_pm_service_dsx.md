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

请注意以下有关 Machine Learning 服务的重要信息。

## 将服务与 Bluemix 应用程序绑定的步骤

您可以下载 Node.js [样本代码](https://github.com/pmservice/product-line-prediction/blob/master/README.md)来试用 Machine Learning 服务。要创建 Bluemix 应用程序并绑定 Machine Learning 服务，请完成以下步骤。以下示例使用的是 Node.js，因为这是比较常用的运行时。可以使用其他运行时，例如 iOS、Ruby、Perl 或 Java。

请注意，还可以使用 Bluemix 图形界面（而不使用 Cloud Foundry 工具 (cf)）执行步骤 1-3。

1. 使用 `cf create-service` 命令创建服务实例：

   ```
   cf create-service pm-20 Free {local naming}
   ```
   {: codeblock}

   例如：

   ```
   cf create-service pm-20 Free my_wml_free
   ```
   {: codeblock}

   此命令将使用名为 `my_wml_free` 的免费套餐在 Bluemix 空间中创建一个 Machine Learning 服务实例。

2. 使用 `cf create-service-key` 命令创建服务凭证：

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

3. 使用 cf bind-service 命令将服务实例 `my_wml_free` 绑定到应用程序。

   ```
   cf bind-service {AppName} my_wml_free
   ```
   {: codeblock}

   例如：

   ```
   cf bind-service my_app1 my_wml_free
   ```
   {: codeblock}

   此命令将 Machine Learning 服务实例 `my_wml_free` 绑定到 Bluemix 应用程序 `my_app1`。



## Machine Learning 凭证

在您将 Machine Learning 服务实例绑定到 Bluemix 应用程序后，系统会将 Machine Learning 凭证添加到 `VCAP_SERVICES` 环境变量中：

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

   `VCAP_SERVICES` 环境变量包含以下信息：

   * `plan` - 服务供应中使用的 Machine Learning 套餐。
   * `url` - Machine Learning 服务实例的地址。
   * `access_key` - 仅限 SPSS Modeler 流。
   * `instance_id` - Machine Learning 实例唯一标识。
   * `username` 和 `password` - 生成访问令牌以在对此服务实例的所有请求中传递时所需的基本授权。例如，可以使用 curl 生成访问令牌，如下所示：

请求示例：

```
       curl --basic --user {username}:{password} https://ibm-watson-ml.mybluemix.net/v3/identity/token

       输出示例：

       {"token":"**********"}
```
{: codeblock}

   以下 Node.js 代码是有关如何从 `VCAP_SERVICES` 环境变量获取 username 和 password 的示例：

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
