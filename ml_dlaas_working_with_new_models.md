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

# Create a Training Run

Training runs are the organizing principle for conducting deep learning Experiments in {{site.data.keyword.pm_full}}. A typical Experiment may consist of dozens to hundreds of training runs, but each run is defined individually and consists of two parts: (1) your neural network defined using one of the [supported deep learning frameworks](ml_dlaas_supported_framework.html) plus (2) the configuration for how to run your training including the number of GPUs and location of the Object Store containing your dataset.
{: shortdesc}

<p align="center"><img src="images/experiment_to_training_runs_text.png" alt="relation of experiments to training runs"></p>

## Creating a model definition .zip file

Once you've defined your neural network and associated data handling using one of the [supported deep learning frameworks](ml_dlaas_supported_framework.html), then package these files together using the .zip format. For example, if you're model was written in Torch then package your .lua files; if in Caffe then zip the .prototxt file; or if in Tensorflow/Keras/MXNet then zip your .py files.  Other compression formats like gzip, tar, etc. are not supported. Consult the documentation for the Deep Learning framework you wish to use in order to prepare the model definition files.  

<!-- Supposedly this isn't true anymore >> NOTE: All model definition files must be in the first level of the zip file so ensure there are no nested directories in the zip file. -->

For example, a zip file `tf-model.zip` containing the model definition for tensorflow might contain the following:

```
unzip -l tf-model.zip
```
{: codeblock}

Sample Output:

```
Archive:  tf-model.zip
  Length      Date    Time    Name
---------  ---------- -----   ----
     7094  09-21-2017 11:38   convolutional_network.py
     5486  09-19-2017 13:49   input_data.py
---------                     -------
    12580                     2 files
```
{: codeblock}

## Upload training data

Your training data must be [uploaded to a compatible Object Storage service instance](ml_dlaas_object_store.html). The credentials from that Object Storage instance will be used below in your training configuration below. The object store is also used to store the trained model at the end of your training run.

## Creating a training configuration file

The model training definition is a YAML formatted file which contains different fields describing the model to be trained, including the deep learning framework to use, the cloud object storage configuration, the resource requirements, and several arguments (including hyperparameters) required for model execution during training and testing. Below we describe the different fields of the model training file for deep learning, continuing our tensorflow handwriting recognition example.

* `model_definition.name`: You can provide any value to name to help identify your training job after it is launched.  However, this does not have to be unique - the service will assign a unique model-id for each launched training job.
* `model_definition.description`: This is another field that you can use to describe the job.
* `model_definition.author`: This is a string identifying the author - perhaps an e-mail address if you wish.
* `model_definition.framework`: This field provides framework specific information the name and version must match one of the [Supported deep learning frameworks](ml_dlaas_supported_framework.html).
    - `model_definition.framework.name`: Name of framework
    - `model_definition.framework.version`: Version of framework.
* `model_definition.execution`: This field provides information concerning the command to launch the training.
    - `model_definition.execution.command`: This field identifies the main program file along with any arguments that deep learning needs to execute.
    - `model_definition.execution.resourceType`: This field specifies the resources that will be allocated for training and should be one of the following values - small (1 GPU), medium (2 GPUs), large (4 GPUs)
* `training_data`: This section specifies the object store where the data files used to train the model are loaded from.
    - `connection`: The connection variables for the data store.
    - `source.type`: Type of data store, currently this can only be set to s3_datastore or bluemix_objectstore.  Use *s3_datastore* if your Object Storage instance is *Cloud Object Storage (control.softlayer.com)* and *bluemix_objectstore* if your Object Storage instance is *Object Storage OpenStack Swift (console.bluemix.net)*.
    - `source.container`: The bucket where the training data resides.
* `training_results`: This section specifies the object store where the resulting model files and logs will be stored after training completes.
    - `connection`: The connection variables for the data store. The list of connection variables supported is data store type dependent.
    - `target.type`: Type of data store, currently this can only be set to s3_datastore or bluemix_objectstore.  Use *s3_datastore* if your Object Storage instance is *Cloud Object Storage (control.softlayer.com)* and *bluemix_objectstore* if your Object Storage instance is *Object Storage OpenStack Swift (console.bluemix.net)*.
    - `target.container`: The bucket where the training results will be written.

For example, the following model training definition file can be used to define a job to train a tensorflow model:

```
model_definition:
  framework:
    name: tensorflow
    version: 1.2-py3
  name: tf-mnist-showtest1
  author: WML User <wmluser@ibm.com>
  description: Simple MNIST model implemented in TF
  execution:
    command: python3 convolutional_network.py --trainImagesFile ${DATA_DIR}/train-images-idx3-ubyte.gz
      --trainLabelsFile ${DATA_DIR}/train-labels-idx1-ubyte.gz --testImagesFile ${DATA_DIR}/t10k-images-idx3-ubyte.gz
      --testLabelsFile ${DATA_DIR}/t10k-labels-idx1-ubyte.gz --learningRate 0.001
      --trainingIters 2000000
    resourceType: small
training_data:
- connection:
    auth_url: <auth-url>
    userId: <username>
    password: <password>
  source:
    container: mnist-training-data
    type: s3_datastore
training_results:
  connection:
    auth_url: <auth-url>
    userId: <username>
    password: <password>
  target:
    container: mnist-training-models
    type: s3_datastore
```
{: codeblock]

where `convolutional_network.py` is the tensorflow program (that is part of the model definition zip) to execute while the remainder are arguments to the program.  Program arguments `--trainImagesFile train-images-idx3-ubyte.gz`, `--trainLabelsFile train-labels-idx1-ubyte.gz`, `--testImagesFile t10k-images-idx3-ubyte.gz`, `--testLabelsFile t10k-labels-idx1-ubyte.gz` values refer to the data set paths in the object store container `tf_training_data`. Program arguments `--trainingIters 20000` and `--learningRate 0.001` pass the values of hyperparameters.

**Note**: When training configuration or model definition files refers to files uploaded to the Object Storage instance, the references should use relative paths as shown above.

**Note**: Before training begins, all files within the training data bucket are downloaded to the training environment operated by the service.  To avoid the overhead/delay of transferring unnecessary files, keep files not used for training files in separate buckets.

## Submit a training run

Once the model definition zip and training configuration files have been prepared, the job can be submitted using the cli command `bx ml train <path-to-model-definition-zip> <path-to-model-configuration-yaml>` and if submitted successfully a unique model-id will be returned:

```
bx ml train tf-model.zip job.yaml
```
{: codeblock}

Sample Output:

```
Starting to train ...
OK
Model-ID is 'training-DOl4q2LkR'
```

# Monitor a training run

To list all training jobs (whether completed or not) use the cli command `bx ml list trained-models`

```
bx ml list trained-models
```
{: codeblock}

Sample Output:

```
Fetching the list of trained models ...
SI No   Name                       guid                 status    submitted-at
1       tf-mnist                   training-DOl4q2LkR   pending   2017-10-26T11:16:51Z

1 records found.
OK
List all trained-models successful
```
{: codeblock}

**Note**: The service will only retain details of training jobs for 7 days after which time they will be removed and will not appear in this list.

To monitor a particular job use the cli command `bx ml show trained-models <model-id>`:

```
bx ml show trained-models training-DOl4q2LkR
```
{: codeblock}

Sample Output:

```
Fetching the trained model details with MODEL-ID 'training-DOl4q2LkR' ...
ModelId        training-DOl4q2LkR
url            /v3/models/training-DOl4q2LkR
Name           tf-mnist
State          running
Submitted_at   2017-10-26T11:10:37Z
OK
Show trained-models details successful
```
{: codeblock}

**Note**: There is currently a known issue with failed jobs disappearing from the list and show command output, as if the job had been deleted.  This issue will be corrected but in the meantime, if you see a training job disappear, please check the training log files as explained below to find out why the job failed.

When a job has completed successfully (or failed) the trained model files and logs should be written to the Cloud Object Storage bucket specified in the setting `training_results` within the model training definition file, under a folder with the same name as the model id.

## Delete a training run

To delete a training job (this will not remove the trained model and logs that were output to your Object Storage instance but rather remove all history of the training job from the service)

```
bx ml delete trained-models training-DOl4q2LkR
```
{: codeblock}


Sample Output:

```
Deleting the trained model 'training-DOl4q2LkR' ...
OK
Delete trained-models successful
```
{: codeblock}
