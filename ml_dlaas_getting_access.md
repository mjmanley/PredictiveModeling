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
# Setting up your machine learning environment and retrieving your credentials

To use IBM Watson Machine Learning you must be able to create the proper machine learning environment and retrieve the credentials that are specific to that environment.

## Setting up your environment

To use IBM Watson Machine Learning you must set up instances of the following items in your IBM Cloud dashboard:

- Watson Machine Learning
- Object Storage
- Apache Spark

In addition to the required instances, some of our notebooks and tutorials also use the following instances. To use those tutorials, you must set these up as well.

- Python Flask
- Natural Language Understanding
- Deep learning experiments

### Creating {{site.data.keyword.Bluemix_notm}} instances

Watch this video to see how to create the {{site.data.keyword.Bluemix_notm}} instances and view the credentials. Then follow the steps below the video to set up your own environment. See the <a href="#retrieving-your-credentials">Retrieving your credentials</a> section below for the steps to view your credentials.

<iframe width="560" height="315" src="https://www.youtube.com/embed/fm8gqguFD9g?rel=0" frameborder="0" allowfullscreen></iframe>

To create Watson Data Platform instances, you must perform the following steps:

1. [Log in to IBM Cloud](https://console.ng.bluemix.net/?cm_sp=dw-bluemix-_-clouddataservices-_-devcenter).
2. From the navigation panel, click **Data & Analytics**.

   You see a screen centered on data services. You can return here regularly to work with your data and analytics services from one easy-to-use page.

3. Click the **Analytics** tab, and then click **Instances**.
4. Click **New Instance**.
5. Configure instances and data storage.

   Enter a descriptive name for your instance, choose a space, and select your data plan (find plan comparison and pricing details on this page).
{{site.data.keyword.Bluemix_notm}} automatically populates the Object storage name with your instance name. It’s likely you’ll need data storage for your Spark project, so choose a space and plan here too.

6. Click **Create Instance**.

Your instance opens.

### Adding existing {{site.data.keyword.Bluemix_notm}} instances to a project in Data Science Experience

Watch this video to see how to create a project and set it up to use Watson Machine Learning.

<iframe width="560" height="315" src="https://www.youtube.com/embed/q3UYBirg4U4?rel=0" frameborder="0" allowfullscreen></iframe>

If you already have instances, but have not linked them to a project in Data Science Experience, you must perform the following steps:

1. [Log on to IBM Data Science Experience](https://datascience.ibm.com).
2. Click **Projects** > **View All Projects**.
3. Click the **Settings** tab.
4. To add a service, in the **Associated Services** panel, click **add associated service**, select a service, complete the configuration information, and click **Save**.
5. To add an access token, perform the following steps:
   6. In the **Access Tokens** panel, click **create new token**. 
   7. In the **Name** box, type a name. 
   8. In the **Access Role For Project** box, select a role, either **Viewer** or **Editor**. 
   9. Click **Add**.
   
6. To connect to a GitHub repository, in the **Repository URL** type your repository location. If you do not have a personal access token already set up for GitHub access, you must create it now by clicking **Settings**. When you have finished, click **Add**.


## Retrieving your credentials

To use your {{site.data.keyword.Bluemix_notm}} instances, services, and models in notebooks and applications, you must be able to insert your credentials, tokens, and scoring endpoints into the code that is used for processing.

1. [Log in to {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/?cm_sp=dw-bluemix-_-clouddataservices-_-devcenter).
2. Scroll to the **Services** section and click the service name whose credentials you want to retrieve.
3. In the navigation pane, click **Service credentials**.
4. In the list of credentials, click **View credentials**.
5. If no credentials exist for this service, you can create them by clicking **Create credentials**.
6. To copy the credentials, click the copy icon.

Depending on the service, you may have different fields, such as `username` and `password`. You must copy the values as they appear to use them in your code.
## Learn more

- [Python Flask]()
- [Natural Language Understanding]()
- [Deep learning experiments](ml_dlaas_environment.html)

[A quick deep learning tutorial](https://www.ibm.com/blogs/watson/2016/10/quick-deep-learning-tutorial/)

