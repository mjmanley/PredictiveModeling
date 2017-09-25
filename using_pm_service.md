---

copyright:
  years: 2016, 2017
lastupdated: "2017-09-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using the service

The modeling methods available on the SPSS Modeler modeling
palette enable you to derive new information from your data and
to develop predictive models. Each method has certain strengths
and is best suited for particular types of problems.
{: .shortdesc}

For details
about SPSS Modeler and the modeling algorithms it provides, see
[IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7).

After the input and output requirements of your Bluemix
application and SPSS Modeler scoring branch design are
implemented, your Data Analyst can change any internal aspect of
the scoring branch. The Data Analyst can even change the model
algorithm(s) used in a refresh operation, ensuring your ability
to fine-tune your predictive analytics without needing to rewrite
your applications.


## Steps to bind the service with Bluemix application
Complete the following steps to create your Bluemix application and bind it to the Machine Learning service.

1. Download Node.js sample application code from [github repository](https://github.com/pmservice/customer-satisfaction-prediction).

2. Use the cf create-service command to create a service
   instance:

   ```
   cf create-service pm-20 Free {local naming}
   ```
   {: codeblock}

   For example:

   ```
   cf create-service pm-20 Free my_pm_free
   ```
   {: codeblock}

   This command creates one Machine Learning service instance
   with Free plan named my_pm_free in your Bluemix space.

3. Use the `cf create-service-key` command to create service
   credentials:

   ```
   cf create-service-key "{service instance name}" {vcap key name}
   ```
   {: codeblock}

   For example:

   ```
   cf create-service-key "IBM Watson Machine Learning - my instance" Credentials-1
   ```
   {: codeblock}

   This command creates Machine Learning service credentials.

4. Use the cf bind-service command to bind the service instance
   my_pm_free to your application.

   ```
   cf bind-service AppName my_pm_service
   ```
   {: codeblock}

   For example:

   ```
   cf bind-service my_app1 my_pm_free
   ```
   {: codeblock}

   This command binds the Machine Learning service instance
   `my_pm_free` to the Bluemix application my_app1.

5. Machine Learning credentials:

   After you bind the Machine Learning service instance to your
   Bluemix application, the Machine Learning credentials are
   added to the `VCAP_SERVICES` environment variable:

```
    {   
        "pm-20": {      
            "name": "pm20-1",
            "label": "pm-20",
            "plan": "Free",
            "credentials": {
                "url": "https://ibm-watson-ml.mybluemix.net",
                "access_key": "XXXXXXXXXXXXX"
            }
        }       
    }
```
{: codeblock}

   The `VCAP_SERVICES` environment variable includes the following
   information:

   <dl>

   <dt>plan</dt>
   <dd>The Machine Learning plan that is used in the service provisioning.</dd>

   <dt>url</dt>
   <dd>The address of the Machine Learning service instance.</dd>

   <dt>access_key</dt>
   <dd>The query parameter accessKey to pass in all requests
            to this service instance.</dd>

   </dl>

For example:             

```
Get https://ibm-watson-ml.mybluemix.net/pm/v1/model/sales_model2?accesskey=XXXXXXXXXXXXX
```
{: codeblock}

   Example Node.js code that shows how to obtain the accessKey
   from the `VCAP_SERVICES` environment variable:

```
   if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var credentials = env['pm-20'][0].credentials;
        var accessKey = credentials.access_key;
    }
```
{: codeblock}
