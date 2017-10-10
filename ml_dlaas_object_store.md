---

copyright:
  years: 2016, 2017
lastupdated: "2017-10-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Object Store for deep learning

<<<<<<< HEAD
To work with the {{site.data.keyword.pm_full}} service and the deep learning components that are part of that service, you must have access to an object store.
{: shortdesc}## Machine Learning Object Store### Creating Object Store instance
1. Go to the {{site.data.keyword.Bluemix_short}} labs Catalog and find the service titled **Cloud Object Storage** in the **Storage** services section.2. Configure your Object Storage instance (recommend {{site.data.keyword.Bluemix_short}} Object Storage Swift) and click **Create**.3. After the service is created, in the side menu, click **Service Credentials** to identify your API URL, user name and password to access the deep learning Service.### Accessing the Object Store instance
The Object Storage service is based on OpenStack Swift and can be accessed by using any compatible client application for accessing the Object Storage APIs.
=======
To work with the {{site.data.keyword.pm_full}} service and the deep learning components that are part of that service, you must have access to a Cloud  Object Storage instance.
{: shortdesc}

## {{site.data.keyword.Bluemix_short}} Cloud Object Store### Creating a Cloud Object Storage instance
1. Go to the {{site.data.keyword.Bluemix_short}} labs Catalog and find the service titled **Cloud Object Storage** in the **Storage** services section.2. Configure your Object Storage instance (recommend {{site.data.keyword.Bluemix_short}} Object Storage Swift) and click **Create**.3. After the service is created, in the side menu, click **Service Credentials** to identify your API URL, user name and password to access the deep learning Service.### Accessing the Cloud Object Storage instance (TODO needs clarification - this is not correct)
The Cloud Object Storage service is based on OpenStack Swift and can be accessed by using any compatible client application for accessing the Object Storage APIs.
>>>>>>> origin/staging
1. Using Python Swift Client: Follow instructions at {{site.data.keyword.Bluemix_short}} Public Object Storage to install the swift client. 
2. Set up your environment and store data on your {{site.data.keyword.Bluemix_short}} Object Storage instance.**Note**: With the free service instance, you are limited to 5GB of data. To accommodate larger data sets, must use the standard service instance.## Learn more

[A quick deep learning tutorial](https://www.ibm.com/blogs/watson/2016/10/quick-deep-learning-tutorial/)


