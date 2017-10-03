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

# Building predictive analytics applications

This section describes the process for deploying and using a
sample Node.js application using the {{site.data.keyword.pm_full}} service.
{: shortdesc}

**Scenario name**: Product line prediction.

**Scenario description**: Our client is running one of the most
famous chain stores in Europe. They would like us to figure out
their clients' interests in terms of their product line such as
Personal Accessories, Camping Equipment, and Outdoor Protection.
A Data Scientist develops a predictive model and shares it with
you (the developer). Your task is to prepare and deploy the
Node.js application that recommends sport product lines by making
score requests against the deployed model.

1. Log on to {{site.data.keyword.Bluemix_short}} and create an instance of {{site.data.keyword.pm_full}}.

2. Launch the {{site.data.keyword.pm_full}} Dashboard.

3. Go to the Samples tab.

4. In the Sample Models section, find the Product Line Prediction
   tile and click the Add model button (+). Now you'll see the
   sample Product Line Prediction model in the list of available
   models on the Models tab.

   **Note**: If you want to use your own Data Science Experience
   project and models instead of the samples, you must persist a
   custom model in the {{site.data.keyword.pm_short}} repository. You can do
   this by either using the REST API or client libraries. For
   details, see Development and persistence of the custom model.

5. From the Action menu, select Create Deployment to deploy the
   Product Line Prediction model as an online deployment.

6. Specify the deployment name (for example, Product line
   prediction) and click Save.You should now see the Product line
   prediction deployment in the Deployments list.

7. From the Action menu, select View Details for your deployment.
   The Scoring Endpoint presented in the details pane will be
   used to run scoring requests.

8. To run scoring requests through the REST API, a scoring
   endpoint and an authorization token are required. For more
   information, see Deploying online models.

9. You can now experiment with the sample Node.js application
   available at
   https://github.com/pmservice/product-line-prediction.

   To automatically deploy sample application code to your
   {{site.data.keyword.Bluemix_short}} space, go to the Samples tab, and in the Sample
   Applications section, select the Product Line Prediction
   application and deploy it by clicking the (+) button.
   Authenticate on the DeployToBluemix form if prompted.

   You should now see the sample application on the {{site.data.keyword.Bluemix_short}}
   Dashboard in the All Apps section.

10. Click the application to view its details. Here you can
    modify application details such as the number of instances,
    memory, etc.

11. Now you can bind your application with the {{site.data.keyword.pm_short}}
    instance. On the Connections tab, click Connect existing.
    After restaging, your application is connected to the service
    instance.

12. Run the application using the route address.

13. In the application, select your Product Line Prediction
    deployment. You are now ready to play with sample records and
    prediction results.
    
## Learn more

Ready to get started? To create an instance of a service or bind
an application, see [Using the service with Spark and Python models](using_pm_service_dsx.html) or
[Using the service with SPSS models](using_pm_service.html).

If you are interested in exploring the API, see [Service API for Spark and Python models](pm_service_api_spark.html) or [Service
API for SPSS models](pm_service_api_spss.html).

For details about SPSS Modeler and the modeling algorithms it
provides, see [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7).

For details about IBM Data Science Experience and the modeling
algorithms it provides, see [https://datascience.ibm.com](https://datascience.ibm.com).