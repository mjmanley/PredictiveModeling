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

# Using the service

To make use of the {{site.data.keyword.pm_short}} service in your application, you must bind the service to the {{site.data.keyword.Bluemix_notm}} application and insert the necessary credentials to run the applicaiton into the `VCAP_SERVICES` environmental variable. 
{: shortdesc}

## Steps to bind the service with {{site.data.keyword.Bluemix_notm}} application

You can download Node.js [sample code](https://github.com/pmservice/product-line-prediction/blob/master/README.md) to try the Machine
Learning service. Complete the following steps to create your {{site.data.keyword.Bluemix_notm}} application and bind the {{site.data.keyword.pm_short}} service. These examples use Node.js because it is a popular runtime. Others can be used such as iOS, Ruby, Perl, or Java.

You can also perform steps 1 - 3 by using the {{site.data.keyword.Bluemix_notm}} Graphical Interface instead of the Cloud Foundry tool (cf).

1. Use the `cf create-service` command to create a service instance:

   ```
   cf create-service pm-20 Free {local naming}
   ```
   {: codeblock}

   For example:

   ```
   cf create-service pm-20 Free my_wml_free
   ```
   {: codeblock}

   This command creates one {{site.data.keyword.pm_short}} service instance
   with the Free plan named `my_wml_free` in your {{site.data.keyword.Bluemix_notm}} space.

2. Use the `cf create-service-key` command to create service
   credentials:

   ```
   cf create-service-key "{service instance name}" {vcap key name}
   ```
   {: codeblock}

   For example:

   ```
   cf create-service-key "IBM {{site.data.keyword.pm_full}} - my instance" Credentials-1
   ```
   {: codeblock}

   This command creates {{site.data.keyword.pm_short}} service credentials.

3. Use the cf bind-service command to bind the service instance
   `my_wml_free` to your application.

   ```
   cf bind-service {AppName} my_wml_free
   ```
   {: codeblock}

   For example:

   ```
   cf bind-service my_app1 my_wml_free
   ```
   {: codeblock}

   This command binds the {{site.data.keyword.pm_short}} service instance
   `my_wml_free` to the {{site.data.keyword.Bluemix_notm}} application `my_app1`.



## IBM Watson Machine Learning credentials

After you bind the {{site.data.keyword.pm_short}} service instance to your {{site.data.keyword.Bluemix}} application, the {{site.data.keyword.pm_short}} credentials are added to the `VCAP_SERVICES` environment variable:

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

   The `VCAP_SERVICES` environment variable includes the following
   information:

   * `plan` - the {{site.data.keyword.pm_short}} plan that is used in the service provisioning.
   * `url` - the address of the {{site.data.keyword.pm_short}} service instance.
   * `access_key` - for IBM® SPSS® Modeler streams only.
   * `instance_id` - {{site.data.keyword.pm_short}} instance unique identifier.
   * `username`, `password` - basic authorization needed to generate an access token to pass in all requests to this service instance. For example, you can generate an access token using a curl like this:

Request example:

```
       curl --basic --user {username}:{password} https://ibm-watson-ml.mybluemix.net/v3/identity/token

       Output example:

       {"token":"**********"}
```
{: codeblock}

   The following Node.js code is an example of how to obtain the
   username and password from the `VCAP_SERVICES` environment
   variable:

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
