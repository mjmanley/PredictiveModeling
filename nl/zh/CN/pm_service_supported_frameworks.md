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

# 支持的机器学习框架

IBM Watson Machine Learning 服务支持以下框架用于模型生命周期管理过程中的模型开发和验证。


## Spark MLlib
Watson Machine Learning Online、Batch (Beta)、Stream (Beta) Deployment and Scoring 服务支持 Spark MLlib。但仅支持特定的版本和运行时环境。

### 支持的版本
*  Spark 2.0

### 限制：

  *  仅支持分类和回归模型。
  *  不支持包含对定制变换器、用户定义的函数和类的引用的模型。
  * 在此阶段，不支持在 scikit-learn 模型部署请求期间返回的“模式”端点。
  *  Beta 中支持 Spark 模型使用批量和流式部署。如果您想要参与，请将您自己加入[等待列表](https://www.ibm.biz/mlwaitlist)！
  * Beta 中有用于 Spark 模型的持续学习系统。如果您想要参与，请将您自己加入[等待列表](https://www.ibm.biz/mlwaitlist)！

## Scikit-learn
Watson Machine Learning Online Deployment and Scoring 服务支持 scikit-learn。但仅支持特定的版本和运行时环境。

### 支持的版本

- Anaconda 4.2.x for Python 3.5 运行时
- Scikit-Learn 0.17

### Python 运行时

对于需要使用 WML Online Deployment and Scoring 服务进行部署的模型，Python 运行时为 Python 3.5。

在某些情况下，如果模型是在 Python 2.7 运行时中创建的，那么部署可能会失败，原因是 Python 2.7 和 Python 3.5 之间不兼容。

### 支持的 Python 软件包

WML Online Deployment and Scoring 服务支持的 Python 软件包的列表位于[此处](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35)。

### 限制

存在一些限制，其中可能包括以下部分或全部限制：

* 仅支持分类和回归模型。
* 模型只能包含对 Anaconda 4.2.x for Python 3.5 运行时支持的软件包（和软件包版本）的引用。
* 未实现在部署请求期间返回的“模式”端点。
* 在此阶段，预测的可能性不会作为评分请求的响应返回。
* 不支持需要 Pandas Dataframe 作为“predict()”API 的输入类型的模型。
* 不支持包含对定制变换器、用户定义的函数和类的引用的模型。

## XGBoost <span class='tag--beta'>Beta</span>
Watson Machine Learning Online Deployment and Scoring 服务支持 XGBoost。但仅支持特定的版本和运行时环境。

### 支持的版本

- XGBoost 0.6
- Anaconda 4.2.x for Python 3.5 运行时
- Scikit-Learn 0.17

### Python 运行时

对于需要使用 WML Online Deployment and Scoring 服务进行部署的模型，Python 运行时为 Python 3.5。

在某些情况下，如果模型是在 Python 2.7 运行时中创建的，那么部署可能会失败，原因是 Python 2.7 和 Python 3.5 之间不兼容。

### 支持的 Python 软件包

WML Online Deployment and Scoring 服务支持的 Python 软件包的列表位于[此处](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35)。

### 限制

存在一些限制，其中可能包括以下部分或全部限制：
* 当前，XGBoost 支持适用于使用 XGBoost 的 Scikit-Learn 包装器（即 xgboot.sklearn_XGBClassifier 和 xgboot.sklearn_XGBRegiscos）创建的模型。
* 模型只能包含对 Anaconda 4.2.x for Python 3.5 运行时支持的软件包（和软件包版本）的引用。
* 未实现在部署请求期间返回的“模式”端点。
* 在此阶段，预测的可能性不会作为评分请求的响应返回。
* 不支持包含对定制变换器、用户定义的函数和类的引用的模型。

## SPSS Modeler

Watson Machine Learning Online 和 Batch Deployment and Scoring 服务支持 SPSS Modeler 流。但仅支持特定的版本和运行时环境。

### 支持的版本

*  SPSS Modeler 17.1
*  SPSS Modeler 18.0

### 限制

对于 SPSS Modeler 流，存在以下限制：

*  当评分分支准备使用实时评分时，应评分请求传入的输入数据必须替换设计到评分分支中的源节点，而产生的预测分析输出必须流回响应流（有效地替换评分分支设计中的终端节点）。

*  当评分分支准备在 Bluemix 中实时执行时，它无法要求与外部服务的连接。
例如，IBM Analytical Decision Management 评分分支设计无法包含 IBM SPSS Collaboration 和 Deployment Services 存储库中存储的规则或模型的参考。
*  在 Bluemix 中执行实时评分的评分分支无法要求外部服务。
例如，您无法针对实时需要 IBM SPSS
Analytic Server 和 Apache Hadoop 数据存储库的模型算法进行部署和评分。
*  Machine Learning 支持 Modeler 嵌入式 Python 脚本编制。
由于用于处理流的方法，在 Machine Learning 中运行流之前，存在几个限制。通常，如果用户选择控制流的执行，那么他们将参考分支的终端节点。
对于 Machine Learning，当我们处理流时，会识别 JSON 中将覆盖的节点，然后在流运行之前，执行替换。
这会导致流在脚本中失败，因为参考的输入和导出节点不再存在。
解决方案是使用其他节点的标识，在执行期间唯一识别分支。
这可确保流如嵌入式 Python 脚本中所定义的那样执行。

## 了解更多信息

有关对 IBM SPSS Analytic Server 培训的预测模型的当前支持的更多详细信息，请参阅 [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/) 的 [SPSS Analytic Server](https://www.ibm.com/support/knowledgecenter/SSWLVY) 部分。
