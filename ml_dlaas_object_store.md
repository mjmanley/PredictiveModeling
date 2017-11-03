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

# Set up you deep learning object store

To work with the {{site.data.keyword.pm_full}} service and the deep learning experiments that are part of that service, you must have access to an S3 Cloud  Object Storage instance.  You will need to define Cloud Object Storage buckets to provide the training data and to store the trained model and logs, and you can use the same or separate Cloud Object Storage instances for this purpose.
{: shortdesc}

## Creating a S3 Cloud Object Storage instance

1. Go to the {{site.data.keyword.Bluemix_short}} labs Catalog and find the service titled **S3 Cloud Object Storage** in the **Storage** services section.
2. Configure your S3 Object Storage instance and click **Create**.
3. After the service is created, in the side menu, click **Service Credentials** to identify your API URL, user name and password to access the deep learning Service.

## Accessing the S3 Cloud Object Storage instance

The S3 Cloud Object Storage service provides S3 compatible APIs and can be accessed by using any compatible client application.

1. Install the Amazon Web Services (AWS) command line interface (CLI). For more information, see  [](https://aws.amazon.com/cli/)
2. Configure the credentials for the S3 Cloud Object Store in your AWS credentials file (for linux, located in~/.aws/credentials)

```
...

[ibm_s3_cos]
aws_access_key_id=<USER NAME>
aws_secret_access_key=<PASSWORD>

```
{: codeblock}

You should now be able to use the AWS CLI to list and update buckets and files, specifying the above profile and the IBM S3 Cloud Object Storage endpoint from your credentials.  For example:

```
# list the buckets in the instance
aws --endpoint-url=<API-URL> --profile ibm_s3_cos s3 ls
```
{: codeblock}

## Learn more

[A quick deep learning tutorial](https://www.ibm.com/blogs/watson/2016/10/quick-deep-learning-tutorial/)


