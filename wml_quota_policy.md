---

copyright:
  years: 2016, 2017
lastupdated: "2017-11-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Quota policy

The {{site.data.keyword.pm_full}} Engine enforces quotas on a per-instance basis to ensure appropriate resource allocation and usage. These policies vary according to account profiles, historical service usage, and availability of resources. The quota policy describes limits that are not defined by the pricing plan and **are subject to change without notice**. The following service quota limits are currently active.
{: shortdesc}

## Resource Usage

Resources are limited to the following maximum values:

-  **Max published models**: 200 (Free plan) 1000 (Standard & Professional plans)
-  **Max Spark ML model size**: 200 MB
-  **Max deployed models**: 1000 (Standard & Professional plans)

**Note**: To understand Free Plan limits, see the description of the [Free Plan](https://console.bluemix.net/catalog/services/machine-learning) in the [{{site.data.keyword.Bluemix_notm}} Catalog](https://console.bluemix.net/catalog/).

## Service Request Limits

You are limited in the number of requests that you can make per minute to specific APIs. If your application needs higher limits, you must [contact {{site.data.keyword.Bluemix_notm}} Support](https://support.ng.bluemix.net/) to increase your quota.

## Deployment requests

The following limits apply to deployment API requests:

-  **Period**: 60 seconds
-  **Default limit**: 10

## Online prediction requests

The following limits apply to [online predictions](pm_service_api_spark_building.html) requests:

-  **Period**: 60 seconds
-  **Default limit**: 500

## Resource management requests

The following limits apply to the combined total requests in this list:

[Token](https://watson-ml-api.mybluemix.net/#/Token): post, get, delete, put, patch requests

[Deployments](https://watson-ml-api.mybluemix.net/#/Deployments): post, get, delete, put, patch requests

-  **Period**: 60 seconds
-  **Default limit**: 100

## Learn more

Ready to get started? To create an instance of a service or bind
an application, see [Using the service with Spark and Python models](using_pm_service_dsx.html) or
[Using the service with IBM® SPSS® models](using_pm_service.html).

If you are interested in exploring the API, see [Service API for Spark and Python models](pm_service_api_spark.html) or [Service
API for IBM® SPSS® models](pm_service_api_spss.html).

For details about IBM® SPSS® Modeler and the modeling algorithms it
provides, see [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7).

For details about IBM Data Science Experience and the modeling
algorithms it provides, see [https://datascience.ibm.com](https://datascience.ibm.com).