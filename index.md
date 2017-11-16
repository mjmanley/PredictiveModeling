---

copyright:
  years: 2016, 2017
lastupdated: "2017-11-16"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started
{: #WMLgettingstarted}

<!--  How to use WML with DSX
- How to use WML with SPSS (Both of these users will be sent to this topic for help and the user needs to find their specific information here
- We need to outline all of the frameworks and APIs that are active and include them in the steps. We will create a highlevel overview and then refer users out to the specfics in the topics

**Notes about structure**: Certain aspects of the Watson Data Platform documentation are not in our control. For example, the headings for LEARN, HOW TO, REFERENCE, and HELP are set. We can only divvie up our topics into those buckets. Also, in this topic the About section is set and is used by WDP for Google searches

Use {{site.data.keyword.pm_full}} to integrate predictive analytics with your applications. Data scientists use machine learning to develop predictive models, whereas developers use machine learning to create applications that make smarter decisions, solve tough problems, and improve user outcomes.
{: shortdesc}

The IBM Watson Machine Learning co-operates with the Apache Spark as a Service to create batch, stream deployments and for learning configuration functionality.

Application runtime environments that you can use , SDK for Node.js, Liberty for Java, Go, PHP, Python, Ruby-->

{{site.data.keyword.pm_full}} is an IBM Cloud service that enables users to perform two fundamental operations of machine learning: training and scoring.
{: shortdesc}

- **Training** is the process of refining an algorithm so that it can learn from a data set. The output of this operation is called a model. A model encompasses the learned coefficients of mathematical expressions.
- **Scoring** is the operation of predicting an outcome by using a trained model. The output of the scoring operation is another data set containing predicted values.

{{site.data.keyword.pm_full}} is designed to address the needs of two primary personas:

- Data Scientists: Create machine learning pipelines that leverage data transformations and machine learning algorithms. They typically use notebooks or external tooling to train and evaluate their models. Data scientists often collaborate with Data engineers to explore and understand the data.
- Developers: Build intelligent applications that use the predictions output by machine learning models.

Although training is a critical step in the machine learning process, {{site.data.keyword.pm_full}} enables you to streamline the functioning of your models by deploying them and getting actual business value from them over time and through all of their iterations.

## Prerequisites

To use {{site.data.keyword.pm_full}}, from the {{site.data.keyword.Bluemix_short}} catalog, you must create the [service instance here](https://console.bluemix.net/catalog/services/ibm-watson-machine-learning/). This setup enables you to perform the following tasks:

## Steps

1. [Set up your Machine Learning environment.](ml_getting_access.html)
1. [Create and store a model](pm_custom_models.html).
2. [Deploy a model](pm_service_api_spark_online.html).
3. Use the deployed model `scoring endpoint` in your application to [get predictions.](pm_service_api_spark_building.html)

## Using Machine Learning with Data Science Experience

{{site.data.keyword.pm_full}} is integrated with IBM Data Science Experience. You can use Machine Learning API client libraries in Data Science Experience notebooks; you must have a Machine Learning instance to use Model Builder and Flow Editor.

## Using Machine Learning with SPSS Modeler

{{site.data.keyword.pm_full}} is integrated with IBM® SPSS® Modeler. You can use the Machine Learning API to leverage advanced mathematical algorithms.


## Using Machine Learning with your environment

{{site.data.keyword.pm_full}} can be used as a hybrid solution linking your local environment with cloud. You can use the Machine Learning API to publish your models, deploy, and score. For more information, see [DSX: Hybrid Mode](https://medium.com/ibm-data-science-experience/dsx-hybrid-mode-91b580450c5b).

## About

The {{site.data.keyword.pm_full}} service is a set of REST APIs that can be
called from any programming language.

The focus of the {{site.data.keyword.pm_full}} service is deployment, but you can use IBM® SPSS® Modeler or IBM® Data Science Experience to author and work with models and pipelines. Both SPSS® Modeler and Data Science Experience that use Spark MLlib and Python scikit-learn offer various modeling methods that are taken from machine learning, artificial intelligence, and statistics.

## Related Links

Ready to get started? To create an instance of a service or bind
an application, see [Using the service with Spark and Python models](using_pm_service_dsx.html) or
[Using the service with SPSS models](using_pm_service.html).

For more information about the API, see [Service API for Spark and Python models](pm_service_api_spark.html) or [Service
API for SPSS models](pm_service_api_spss.html).

For more information about IBM® SPSS® Modeler and the modeling algorithms it
provides, see [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7).

For more information about IBM Data Science Experience and the modeling
algorithms it provides, see [https://datascience.ibm.com](https://datascience.ibm.com).
