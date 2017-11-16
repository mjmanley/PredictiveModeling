---

copyright:
  years: 2016, 2017
lastupdated: "2017-11-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Setup an object store for deep learning

To work with the {{site.data.keyword.pm_full}} service and the deep learning experiments that are part of that service, you must have access to a Cloud Object Storage (control.softlayer.com) or Object Storage OpenStack Swift (console.bluemix.net) instance.  You will need to define Cloud Object Storage buckets to provide the training data and to store the trained model and logs, and you can use the same or separate Cloud Object Storage instances for this purpose.
{: shortdesc}

## Creating an Cloud Object Storage instance

1. Go to the {{site.data.keyword.Bluemix_short}} labs Catalog and find the either service titled **Cloud Object Storage (control.softlayer.com)** or the service titled **Object Storage OpenStack Swift (console.bluemix.net)** in the **Storage** services section.
2. Configure your Object Storage instance and click **Create**.
3. After the service is created, in the side menu, click **Service Credentials** to obtain the credentials including API URL, user name and password to access the Object Storage instance.

## Accessing the Cloud Object Storage (control.softlayer.com) instance

The Cloud Object Storage (IaaS) service provides S3 compatible APIs and can be accessed by using any compatible client application.

1. Install the Amazon Web Services (AWS) command line interface (CLI). For more information, see  [](https://aws.amazon.com/cli/)
2. Configure the credentials for the Cloud Object Storage (IaaS) in your AWS credentials file (for linux, located in ~/.aws/credentials)

```
...

[ibm_s3_cos]
aws_access_key_id=<USER NAME>
aws_secret_access_key=<PASSWORD>

```
{: codeblock}

You should now be able to use the AWS CLI to list and update buckets and files, specifying the above profile and the Cloud Object Storage endpoint from your credentials.  For example:

```
# list the buckets in the instance
aws --endpoint-url=<API-URL> --profile ibm_s3_cos s3 ls
```
{: codeblock}

## Accessing the Object Storage OpenStack Swift (console.bluemix.net) instance

You can use the swift CLI or client libraries (for example the swift python client library to access this objectstore).  For more details please refer to [the documentation](https://console.bluemix.net/docs/services/ObjectStorage/index.html)

## Data formatting

Different frameworks require train and test data sets in different formats. For example, Caffe requires data sets in LevelDB or LMDB format while Torch requires data sets in Torch proprietary format. We assume that data is already in the format needed by the specific framework. Details on how to convert raw data to framework specific format is beyond the scope of this document. Consult the documentation for the deep learning framework you wish to use for more information.
