---

copyright:
  years: 2016, 2017
lastupdated: "2017-11-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
# Setting up your environment

To use IBM Watson Machine Learning you must be able to create the proper machine learning environment and retrieve the credentials that are specific to that environment.
You can create {{site.data.keyword.Bluemix_notm}} instance either by using [Cloud Foundry CLI](https://github.com/cloudfoundry/cli#getting-started) or through {{site.data.keyword.Bluemix_notm}} graphical interface (Dashboard).


## Graphical interface
### Creating {{site.data.keyword.Bluemix_notm}} instances

To use IBM Watson Machine Learning you must [create an instance](https://console.bluemix.net/catalog/services/machine-learning) of it in your IBM Cloud dashboard.

Depending on your scenario you may also need:
- Object Storage (batch deployment)
- DB2 Warehouse on Cloud (batch deployment)
- Apache Spark (batch, stream deployment and continuous learning system)
- Message Hub (stream deployment)

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


To make use of the {{site.data.keyword.pm_short}} service in your application, you must bind the service to the {{site.data.keyword.Bluemix_notm}} application and the necessary credentials to run the applicaiton are inserted into the `VCAP_SERVICES` environmental variable. For more details refer to <a href="#Cloud-Foundry-CLI">Cloud Foundry CLI</a> section.
{: shortdesc}



## Cloud Foundry CLI

### Steps to bind the service with {{site.data.keyword.Bluemix_notm}} application

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



### Accessing credentials through `VCAP_SERVICES`variable

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
