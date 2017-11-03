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

# Set up deep learning experiments

To work with deep learning experiments within the Watson Machine Learning service, you must set up your environment. You can train deep learning experiments through a command line interface.
{: shortdesc}

## Access deep learning experiments by using the command line interface

It is possible to train deep learning models through the use of a command line interface (CLI) which will allow you to create and monitor deep learning model training jobs.

### Install the command line interface 
 
1.  Install the [command line interface](http://clis.ng.bluemix.net/ui/home.html), which as its instructions explain pre-reqs installing the [CLI](https://console.stage1.ng.bluemix.net/docs/starters/install_cli.html)
2.  Download a version of the WML CLI plugin from the [releases ](https://github.ibm.com/NGP-TWC/wml-cli/releases) page of this repository. Be sure to get the right version for your platform.


And once we are GA ready the wml-cli binaries will be available at the
https://plugins.ng.bluemix.net/ui/repository.html#bluemix-plugins
This is location where all bluemix cli for various services are made available.

3. Install CLI plugin using either of these commands
```
# For the most recent version of the plugin
bx plugin install ml_cli_plugin

# Or to install a specific version
bx plugin install https://github.ibm.com/NGP-TWC/wml-cli/releases/<binary_name>
```

    ```
    $ bx plugin install path/to/wml_cli_plugin_xxx
    Installing plugin...
    OK
    Plug-in 'deep-learning 0.1.0' was successfully installed into /Users/me/.bluemix/plugins/deep-learning.
    ```
    {: codeblock}
    
4.  Verify the CLI plugin is installed

    ```
    $ bx dl help
    NAME:
   bx dl - Manage deep learning models on Bluemix
    USAGE:
   bx dl command [arguments...] [command options]

    COMMANDS:
   init       Creates a new deep learning project with a manifest.
   train      Trains a model
   show       Get detailed information about a model and training status
   delete     Delete a model
   list       List all models
   download   Download the model definition as ZIP file
   logs       View the ongoing training logs
   halt       Halt a training job
   version    show git hash and build time of cli
   help       
   
    Enter 'bx dl help [command]' for more information about a command.
    ```
    {: codeblock}
    
You can now use the deep learning experiments CLI plugin. Before using the plugin for model deployment and training you need to create an instance on Watson Data Platform and set up your environment variables. For more information, see [Creating a deep learning instance on {{site.data.keyword.Bluemix_notm}}](#51--creating-dlaas-instance-on-bluemix) and [Environment Set-up](#52-environment-set-up). 

### Model Training 

#### Connect to IBM Watson Data Platform

```
$ bx api https://api.stage1.ng.bluemix.net
```
{: codeblock}

#### Create a project template

Create a `manifest.yml` template file that's used to describe your deep learning project. 

```
$ bx dl init --h
NAME:
   init - Creates a new deep learning project with a manifest.

USAGE:
   bx dl init NAME
```
{: codeblock}

For example, to create a caffe project with version 1 of caffe us the following command

```
$ bx dl init foo
```
{: codeblock}

You'll find a `manifest.yml` template file in the `foo` directory. The manifest file contains different fields describing the DLaaS model, its object store information, its resource requirements, and several arguments (including hyperparameters) required for model execution during training and testing. For more information on manifest file and its different fields refer to [6.3 Creating Manifest file](#63-creating-manifest-file) 

#### Train the model

```
$ bx dl train --h
NAME:
   train - Trains a model

USAGE:
   bx dl train MANIFEST_FILE (MODEL_DEFINITION_ZIP|MODEL_DEFINITION_DIR)
```
{: codeblock}

You need to specify the manifest file and either a ZIP file containing your model definition files or the directory name containing your model definition files. For illustration purpose, commands below are for an example mnist caffe model. You need to specify your model specific files for executing these commands for your model. 
2.  Download a version of the CLI plugin from the [ML CLI releases](https://github.ibm.com/NGP-TWC/wml-cli/releases) page of this repository. Be sure to get the right version for your platform.
3. Install CLI plugin (for example on OSX this downloaded as ml_cli_plugin_osx)

```
$ bx plugin install ml_cli_plugin_osx
Installing binary...
OK
Plug-in 'machine-learning 1.0.0' was successfully installed into /Users/username/.bluemix/plugins/machine-learning. Use 'bx plugin show machine-learning' to show its details.
```
{: codeblock}
    
4.  Verify the CLI plugin is installed

```
$ bx ml help
NAME:
   bx ml - Manage machine learning lifecycle on Bluemix
USAGE:
   bx ml command [arguments...] [command options]

COMMANDS:
   show      Get detailed information about models/deployments/trained-models
   train     Start training a model
   delete    Delete a deployment/trained-model
   list      List all models/deployments/frameworks/trained-models
   version   show git hash and build time of cli
   deploy    Deploy a model for scoring
   score     Score the model. Sample scoring json format -  {"modelId": "sample", "deploymentId": "sample","payload": {"fields": [],"values": []}}
   help

Enter 'bx ml help [command]' for more information about a command.
```
{: codeblock}
    
You can now use the deep learning experiments CLI plugin. Before using the plugin for model deployment and training you need to create an instance on Watson Data Platform and set up your environment variables. For more information, see [Creating a deep learning instance on {{site.data.keyword.Bluemix_notm}}](#51--creating-dlaas-instance-on-bluemix) and [Environment Set-up](#52-environment-set-up). 

### Model Training 

#### Connect to IBM Watson Data Platform

```
$ bx api https://api.stage1.ng.bluemix.net
$ bx login -u <bluemix-username>
```
{: codeblock}

#### Create a project template

Consult [Working with new deep learning models](ml_dlaas_working_with_new_models.md) for an example of how to use the CLI to train deep learning models.

### CLI Upgrade

Check [ML CLI releases](https://github.ibm.com/NGP-TWC/wml-cli/releases) for new versions of the ML CLI. We encourage you to download the latest release of CLI to have the most up-to date features. After downloading
the latest version of ML CLI for your operating system, you need to uninstall the plugin (if you already have an older
version installed) and then install the new version.
 
```
$ bluemix plugin uninstall "machine-learning"
Uninstalling plug-in 'deep-learning'...
Uninstalling plug-in 'machine-learning'...
OK
Plug-in 'machine-learning' was successfully uninstalled.
$ bluemix plugin install ml_cli_plugin_osx
Installing binary...
OK
Plug-in 'machine-learning 1.0.1' was successfully installed into /Users/username/.bluemix/plugins/machine-learning. Use 'bx plugin show machine-learning' to show its details.
```
{: codeblock}

<!--
## Access deep learning experiments via cURL 

In addition to the command line interface, you can access your deep learning experiments via cURL commands.

### Model Training

Instructions below assume that you already have a zip file containing model definition files of the model to be deployed and the training /test data of the model are already uploaded on DLaaS object store with the credentials and path specified in the manifest file of the model. This is the case if you are working with [DLaaS example models for demo](). If you want to deploy your own models you need to first upload your training and test data to DLaaS object store and then create a manifest file of your model accordingly using instructions at [Working with New Models](). After this, you create a zip file of the model, say test-model.zip containing the model definition files. 

The commands below assume that the manifest file is stored in the same directory with zip file of the model (as you will see in the zip file of example models at [Working with Example Models](). You can have it locally in a separate folder. During deployment time you need to specify its local path. The commands below assume the model is caffe-mnist-model, only for illustration purpose.  

#### Train the model

```
$ curl -u $DLAAS_USERNAME:$DLAAS_PASSWORD -XPOST $DLAAS_URL/v1/models?version=2017-02-13 -F "model_definition=@caffe-mnist-model.zip" -F "manifest=@caffe-mnist-manifest.yml"
{"model_id":"training-MoyTfA7zg","location":"/v1/models/training-MoyTfA7zg"}
```
{: codeblock}

This will deploy and run a model training job on IBM DLaaS cluster. On success, model_id, the id of the model, is returned in the response.  

#### Get information about the model

You can query the model using the model_id obtained above. 

```
$ curl -u $DLAAS_USERNAME:$DLAAS_PASSWORD -XGET $DLAAS_URL/v1/models/training-MoyTfA7zg?version=2017-02-13
{"model_id":"training-MoyTfA7zg","location":"/v1/models/training-MoyTfA7zg/caffe-model-zFPof0nkg","data_stores":[{"connection":{"auth_url":"https://dal05.objectstorage.service.networklayer.com/auth/v1.0/","password":"e739397fbd7d3603679a87a8dcf7b7e66b8892fbcbc233e1d8e8932efd6eed84","user_name":"IBMOS366226-358:dlaas-watson"},"data_store_id":"sl-internal-os","type":"softlayer_objectstore"}],"description":"Caffe MNIST model running on GPUs.","framework":{"name":"caffe","version":"1"},"name":"mnist-caffe-model","training":{"command":"caffe train -solver lenet_solver.prototxt","gpus":1,"input_data":["sl-internal-os"],"memory":500,"memory_unit":"MiB","output_data":["sl-internal-os"],"training_status":{"completed":"2017-04-11 06:47:10.823956475 +0000 UTC","status":"COMPLETED","status_description":"COMPLETED","submitted":"2017-04-11 06:46:46.200475477 +0000 UTC"}}}
```
{: codeblock}

The json response contains details of the model and its status (like `NOT_STARTED`, `DOWNLOADING`, `STORING`, `COMPLETED`...). 

#### Download the model definition

After the training, you can download the model definition that was initial used for training as a ZIP archive.
 
```
$ curl -u $DLAAS_USERNAME:$DLAAS_PASSWORD -XGET $DLAAS_URL/v1/models/training-MoyTfA7zg/definition?version=2017-02-13 -o training-MoyTfA7zg-definition.zip
```
{: codeblock}

#### Download the trained model and log files

After the training is completed you can download the trained model and training log files as ZIP archive. 

```
$ curl -u $DLAAS_USERNAME:$DLAAS_PASSWORD -XGET $DLAAS_URL/v1/models/training-MoyTfA7zg/trained_model?version=2017-02-13 -o training-MoyTfA7zg-trainedmodel.zip
```
{: codeblock}

The download will only work if the size of the trained model is less than 200 MB. Else, you will receive an error message: 

```
Trained model exceeded the download limit. Please download it from your cloud storage directly. 
```
{: codeblock}

#### Delete the model (optional)

```
$ curl -u $DLAAS_USERNAME:$DLAAS_PASSWORD -XDELETE $DLAAS_URL/v1/models/training-MoyTfA7zg?version=2017-02-13
{"model_id":"training-MoyTfA7zg"}
```
{: codeblock}

This deletes an existing model but does not delete any data in the user's data store. The model_id of the deleted model is returned as response. 

## Learn more

[A quick deep learning tutorial](https://www.ibm.com/blogs/watson/2016/10/quick-deep-learning-tutorial/)

