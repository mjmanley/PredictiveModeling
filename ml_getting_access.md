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
# Setting up your Machine Learning environment

To use IBM Watson Machine Learning you must be able to create the proper machine learning environment and retrieve the credentials that are specific to that environment.

## Setting up your environment

To use IBM Watson Machine Learning you must [create an instance](https://console.bluemix.net/catalog/services/machine-learning) of it in your IBM Cloud dashboard.

Depending on your scenario you may also need:
- Object Storage (batch deployment)
- DB2 Warehouse on Cloud (batch deployment)
- Apache Spark (batch, stream deployment and continuous learning system)
- Message Hub (stream deployment)


### Creating {{site.data.keyword.Bluemix_notm}} instances

You can create {{site.data.keyword.Bluemix_notm}} instance either by using [Cloud Foundry CLI](https://github.com/cloudfoundry/cli#getting-started) or through {{site.data.keyword.Bluemix_notm}} Dashboard. If you are interested in CF commands please refer to [using the service](using_pm_service.html) with application section.
If you want to work with Dasboard watch this video to see how to create the {{site.data.keyword.Bluemix_notm}} instances and view the credentials. Then follow the steps below the video to set up your own environment. See the <a href="#retrieving-your-credentials">Retrieving your credentials</a> section below for the steps to view your credentials.

<iframe width="560" height="315" src="https://www.youtube.com/embed/fm8gqguFD9g?rel=0" frameborder="0" allowfullscreen></iframe>

To create Watson Machine Learning instance, you must perform the following steps:

1. Open Watson Machine Learning [service page](https://console.bluemix.net/catalog/services/machine-learning)
2. Sign up or log in to create service instance.
3. Enter a descriptive name for your instance, choose a space, and select your data plan (find plan comparison and pricing details on this page).
4. Click **Create Instance**.

Your instance opens.


### Retrieving your credentials

To use your Bluemix instance you need service instance credentials. You can create and access your credentials either through [CF CLI](using_pm_service.html) or {{site.data.keyword.Bluemix_notm}} Dashboard. Please also note that after you bind the Machine Learning service instance to your IBM® Cloud application, the Machine Learning credentials are added to the VCAP_SERVICES environment variable (refer to [using the service](using_pm_service.html) with application for more details).

To retrieve Watson Machine Learning instance credentials, you must perform the following steps:

1. [Log in to {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/?cm_sp=dw-bluemix-_-clouddataservices-_-devcenter).
2. Scroll to the **Services** section and click the service name whose credentials you want to retrieve.
3. In the navigation pane, click **Service credentials**.
4. In the list of credentials, click **View credentials**.
5. If no credentials exist for this service, you can create them by clicking **Create credentials**.
6. To copy the credentials, click the copy icon.
