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

# Working with new deep learning models

To work with new deep learning models using the {{site.data.keyword.pm_full}} service you first need to create model definition files and data files for training and testing.
{: shortdesc}

## Creating model definition zip

Different deep learning frameworks support different languages to define their models. For example, Torch models are defined in LuaJIT whereas Caffe models are defined by using config files written in Protocol Buffer Language. Tensorflow models are defined using python code.  Please consult the documentation for the Deep Learning framework you wish to use in order to prepare the model definition files.

The file(s) comprising the model definition should be zipped.  At present, deep learning only supports the zip format for model files, other compression formats like gzip, bzip, tar etc., are not supported. Note that all model definition files has to be in the first level of the zip file and there are no nested directories in the zip file.

For example, a zip file ```tf-model.zip``` containing the model definition for tensorflow to build a deep learning model to perform handwritten digit recognition might contain the following files:

```
$ unzip -l tf-model.zip
Archive:  tf-model.zip
  Length      Date    Time    Name
---------  ---------- -----   ----
     7094  09-21-2017 11:38   convolutional_network.py
     5486  09-19-2017 13:49   input_data.py
---------                     -------
    12580                     2 files

```
{: codeblock}

## Training and test data

### Data formatting

Different frameworks require train and test datasets in different formats. For example, Caffe requires datasets in LevelDB or LMDB format while Torch requires datasets in Torch proprietary format. We assume that data is already in the format needed by the specific framework. Details on how to convert raw data to framework specific format is beyond the scope of this document - please consult the documentation for the deep learning framework you wish to use for more information.

### Uploading data to the Object Store

Before uploading your model data in object store you first need to create a compatible cloud object store account/service instance either on {{site.data.keyword.Bluemix_notm}} or on SoftLayer and get the service credentials. For more information, see [Object Store for deep learning](ml_dlaas_object_store.html). You can then use these credentials to create a container in the object store and upload your data. The object store is also used to store the trained model.

## Creating a model training definition file

The model training definition file contains different fields describing the model in deep learning, its object store information, its resource requirements, and several arguments (including hyperparameters) required for model execution during training and testing. Below we describe different fields of the model training file for deep learning, continuing our tensorflow handwriting recognition example.

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
    - `source.type`: Type of data store, currently this can only be set to s3_datastore
    - `source.container`: The container where the training data resides.
* `training_results`: This section specifies the object store where the resulting model files and logs will be stored after training completes.
    - `connection`: The connection variables for the data store. The list of connection variables supported is data store type dependent.
    - `target.type`: Type of data store, currently this can only be set to s3_datastore
    - `target.container`: The container where the training data resides.


For example, the following model training definition file can be used to define a job to train a tensorflow model:

```
{
  "model_definition": {
    "framework": {
      "name": "tensorflow",
      "version": "1.2-py3"
    },
    "name": "tf-mnist",
    "author": "Ann Other",
    "description": "Simple MNIST model implemented in TF",
    "execution": {
      "command": "python3 convolutional_network.py --trainImagesFile ${DATA_DIR}/train-images-idx3-ubyte.gz --trainLabelsFile ${DATA_DIR}/train-labels-idx1-ubyte.gz --testImagesFile ${DATA_DIR}/t10k-images-idx3-ubyte.gz --testLabelsFile ${DATA_DIR}/t10k-labels-idx1-ubyte.gz --learningRate 0.001 --trainingIters 20000",
      "resourceType": "small"
    }
  },
  "training_data": [
    {
      "connection": {
        "auth_url": "<url>",
        "userId": "<username>",
        "password": "<password>"
      },
      "source": {
        "container": "tf_training_data",
        "type": "softlayer_objectstore"
      }
    }
  ],
  "training_results":
    {
      "connection": {
         "auth_url": "<url>",
         "userId": "<username>",
         "password": "<password>"
      },
      "target": {
        "container": "tf_training_results",
        "type": "softlayer_objectstore"
      }
    }
}

```
{: codeblock]

where `convolutional_network.py` is the tensorflow program (that is part of the model definition zip) to execute while the remainder are arguments to the program.  Program arguments `--trainImagesFile train-images-idx3-ubyte.gz`, `--trainLabelsFile train-labels-idx1-ubyte.gz`, `--testImagesFile t10k-images-idx3-ubyte.gz`, `--testLabelsFile t10k-labels-idx1-ubyte.gz` values refer to the dataset paths in the objectstore container `tf_training_data`. Program arguments `--trainingIters 20000` and `--learningRate 0.001` pass the values of hyperparameters.

**Note**: Where the user's model training definition and/or model definition files refer to some training data, they shouldn't use absolute paths. They should be specified relative to the environment variable `${DATA_DIR}` as in the command above.

## Submitting the training job

Once the model definition zip and model training definition file has been prepared, the job can be submitted using the cli command To monitor a particular job use the cli command ```bx ml train <path-to-model-definition-zip> <path-to-model-training-definition-json>``` and if submitted successfully a unique model-id will be returned:

```
$ bx ml train tf-model.zip job.json
Starting to train ...
OK
Model-ID is 'training-DOl4q2LkR'
```
{: codeblock}

To list all training jobs (whether completed or not) use the cli command ```bx ml list trained-models```

```
$ bx ml list trained-models
Fetching the list of trained models ...
SI No   Name                       guid                 status    submitted-at
1       tf-mnist                   training-DOl4q2LkR   pending   2017-10-26T11:16:51Z

1 records found.
OK
List all trained-models successful
```
{: codeblock}

To monitor a particular job use the cli command ```bx ml show trained-models <model-id>```:

```
$ bx ml show trained-models training-DOl4q2LkR
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



To delete a training job (this will not remove the trained model and logs that were output to the Cloud Object Storage, but rather remove all history of the training job from the service)

```
$ bx ml delete trained-models training-DOl4q2LkR
Deleting the trained model 'training-DOl4q2LkR' ...
OK
Delete trained-models successful
```
{: codeblock}

## Learn more

Visit 