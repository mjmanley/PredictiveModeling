---

copyright:
  years: 2016, 2017
lastupdated: "2017-11-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Supported frameworks

The {{site.data.keyword.pm_full}} service supports the following frameworks for model development and validation as a part of model life cycle management.
{: shortdesc}

## Spark MLlib

There is support for Spark MLlib for the {{site.data.keyword.pm_full}} Online, Batch (beta), Stream (beta) Deployment and Scoring service. Only specific versions and runtime environments are supported.

### Capabilities
* Deployment types:
  * Online
  * Batch with Object Storage, DB2 Warehouse on Cloud, and DB2 on Cloud
  * Stream with Message Hub
*  Continuous Learning System

### Supported Versions
*  Spark 2.0

### Restrictions

  *  Only classification and regression models are supported.
  *  Models that contain references to custom transformers, user defined functions, and classes are not supported.


## Scikit-learn

There is support for scikit-learn for the {{site.data.keyword.pm_full}} Online Deployment and Scoring service. Only specific versions and runtime environments are supported.

### Capabilities
* Deployment types:
  * Online

### Supported Versions

- Anaconda 4.2.x for Python 3.5 Runtime
- Scikit-Learn 0.17

### Python Runtime

The Python runtime for models that needs to be deployed using WML Online Deployment and Scoring service is Python 3.5.

In some cases, where models were created in Python 2.7 runtime, deployment may fail due to incompatibilities between Python2.7 and Python3.5.

### Supported Python Packages

A list of Python packages supported by WML Online Deployment and Scoring service can be found [here](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35).

### Restrictions

There are some restrictions, which may include some or all of the following limitations:

* Classification and regression models are only supported.
* Models can contain references only to those packages (and package version) supported by Anaconda 4.2.x for Python 3.5 runtime.
* The "schema" endpoint returned during deployment request is not implemented.
* Models that require Pandas Dataframe as input type for "predict()" API are not supported.
* Models that contain references to custom transformers, user defined functions and classes are not supported.

## XGBoost
There is support for XGBoost for the {{site.data.keyword.pm_full}} Online Deployment and Scoring service. Only specific versions and runtime environments are supported.

### Capabilities
* Deployment types:
  * Online

### Supported Versions

- XGBoost 0.6
- Anaconda 4.2.x for Python 3.5 Runtime
- Scikit-Learn 0.17

### Python Runtime

The Python runtime for models that needs to be deployed using WML Online Deployment and Scoring service is Python 3.5.

In some cases, where models were created in Python 2.7 runtime, deployment may fail due to incompatibilities between Python2.7 and Python3.5.

### Supported Python Packages

A list of Python packages supported by WML Online Deployment and Scoring service can be found [here](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35).

### Restrictions

There are some restrictions, which may include some or all of the following limitations:

* Models can contain references only to those packages (and package version) supported by Anaconda 4.2.x for Python 3.5 runtime.
* The "schema" endpoint returned during deployment request is not implemented.
* Probability of prediction is not returned as a response of scoring request at this stage.
* Models containing references to custom transformers, user defined functions and classes are not supported.

## SPSS Modeler

There is support for IBM® SPSS® Modeler streams for the {{site.data.keyword.pm_full}} Online, Batch Deployment and Scoring service. Only specific versions and runtime environments are supported.

### Capabilities
* Deployment types:
  * Online
  * Batch
* Retraining
* Run stream


### Supported Versions

*  IBM® SPSS® Modeler 17.1
*  IBM® SPSS® Modeler 18.0

### Restrictions

The following restrictions exist for IBM® SPSS® Modeler streams:

*  Streams created in the IBM® Data Science Experience Flow Editor are not supported.
*  When a scoring branch is prepared for use in real-time scoring, input data coming in on the score request must replace the source node designed into the scoring branch and the resulting predictive analytic output must flow back into the response flow (effectively replacing the terminal node in the scoring branch design).
*  As the scoring branch is prepared for real-time execution in {{site.data.keyword.Bluemix_short}}, it cannot require a connection to an external service. For example, an IBM Analytical Decision Management scoring branch design cannot contain references to rules or models stored in an IBM® SPSS® Collaboration and Deployment Services repository.
*  The execution of a scoring branch for real-time scoring in {{site.data.keyword.Bluemix_short}} cannot require an external service. For example, you cannot deploy and score against model algorithms that require an IBM® SPSS® Analytic Server and Apache Hadoop data store in real-time.
*  {{site.data.keyword.pm_short}} supports Modeler embedded Python scripting. There are a few restrictions due to the method used for processing streams before they run in {{site.data.keyword.pm_short}}. Typically, if a user chooses to control the execution of the stream, they will reference the terminal node of the branch. For {{site.data.keyword.pm_short}}, when we process the stream, we identify the nodes from JSON that will be overridden, and then do the replacement before the stream runs. This causes the stream to fail in the script because the referenced input and export nodes no longer exist. The solution is use the ID of another node to uniquely identify the branch during execution. This ensures that the stream executes as defined in the embedded Python script.

## Learn more

For more details about current support for IBM® SPSS® Analytic Server-trained predictive models, see the [IBM® SPSS® Analytic Server](https://www.ibm.com/support/knowledgecenter/SSWLVY) section of [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/).
