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

# Working with new deep learning models
To work with new deep learning models using the {{site.data.keyword.pm_full}} service you first need to create model definition files and data files for training and testing.
{: shortdesc}## Creating model zip file to define a training Experiment 
Different deep learning frameworks support different languages to define their models. For example, Torch models are defined in LuaJIT whereas Caffe models are defined by using config files written in Protocol Buffer Language. Tensorflow models are defined using python code.  Details on how to write model definition files is beyond the scope of this document.

The file(s) comprising the model definition should be zipped and the zip file uploaded to a new **experiment**.  At present, deep learning only supports zip format for model files, other compression formats like gzip, bzip, tar etc., are not supported. Note that all model definition files has to be in the first level of the zip file and there are no nested directories in the zip file.You will need to use the URL for the experiment's version in the model training definition file `model_definition.definition_location`.

**TODO reference needed to section on creating repository / experiments or describe that more here **
## Training and test data### Data formattingDifferent frameworks require train and test datasets in different formats. For example, Caffe requires datasets in LevelDB or LMDB format while Torch requires datasets in Torch proprietary format. We assume that data is already in the format needed by the specific framework. Details on how to convert raw data to framework specific format is beyond the scope of this document.### Uploading data to the object StoreBefore uploading your model data in object store you first need to create an object store account/service instance either on Bluemix or on SoftLayer and get the service credentials. For more information, see [Object Store for deep learning](ml_dlaas_object_store.html). You can then use these credentials to create a container in the object store and upload your data. The object store is also used to store the trained model.## Creating a model training definition file
The model training definition file contains different fields describing the model in deep learning , its object store information, its resource requirements, and several arguments (including hyperparameters) required for model execution during training and testing. Here are example model training files for Caffe and TensorFlow models. You can use these templates to create model training file for your models. Below we describe different fields of the model training file for deep learning.
* `model_definition.name`: After a model is deployed in deep learning a unique id for the model is created. The model id is +, where is a string of alphanumeric characters to uniquely identify the deployed model. is a prefix of the model id. You can provide any value to name.* `model_definition.description`: This is for users to keep track of their deployed models. Users can use in future and get information about particular model. deep learning does not interpret it. You can put anything here.* `model_definition.author`: This is a string identifying the author - perhaps an e-mail address.
* `model_definition.definition_location`: This is the URL of the experiment
* `model_definition.framework`: This field provides framework specific information.     - `model_definition.framework.name`: Name of framework, values can be `caffe`, `torch`, or `tensorflow`.    - `model_definition.framework.version`: Version of framework.
* `model_definition.execution`: This field provides information concerning the command to launch the training.    - `model_definition.execution.command`: This field identifies the main program file along with any arguments that deep learning needs to execute. 
    - `model_definition.execution.resourceType`: This field specifies the resources that will be allocated for training and should be one of the following values - small (1 GPU), medium (2 GPUs), large (3 GPUs)
* `training_data`: This section specifies the object store where the data files used to train the model are loaded from.     - `training_data.connection`: The connection variables for the data store. The list of connection variables supported is data store type dependent.    - `type`: Type of data store, values can be ...        - `container`: The container where the training data resides.

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
    "definition_location": "https://ibm-watson-ml.stage1.mybluemix.net/v3/ml_assets/experiments/c7e148f1-a83a-4bf8-a69c-fa815480cd15/versions/8cd6a2fc-f64b-4af5-bad8-6d623001aee6",
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
  ]
}

```
{: codeblock]

<<<<<<< HEAD
where `cnn.lua` is the model code to execute while the remainder are arguments to the model. The `trainFile`, `validFile`, `testFile`, `embeddingFile` values refer to the dataset path in the `learner`, `numLabels`, `epoch`, `batchSize`, `learningRate`, and `saveMode` training parameters and hyperparameters, and `outputprefix` refers to the output directory path in the `learner` data path.
**Note**: If the user's model and manifest files refer to some training data, they shouldn't use absolute paths. They should use either the relative paths or the environment variables.* To use relative paths, enter the following values:   -trainFile `./yelp_train_500k`  -validFile `./yelp_valid_2000`  -testFile  `./yelp_test_2000`* To use the $DATA environment variable, enter the following values:   -trainFile: `${DATA_DIR}/yelp_train_500k`  -validFile: `${DATA_DIR}/yelp_valid_2000`  -testFile: `${DATA_DIR}/yelp_test_2000`## Creating model zip file
You need to zip all the model definition files and create a model zip file. At present, deep learning only supports zip format for model files, other compression formats like gzip, bzip, tar etc., are not supported. Note that all model definition files has to be in the first level of the zip file and there are no nested directories in the zip file.## Model deployment and trainingAfter creating the manifest file and model zip file refer to instructions under Using deep learning via Bluemix for working with your model in deep learning.## Learn more

[A quick deep learning tutorial](https://www.ibm.com/blogs/watson/2016/10/quick-deep-learning-tutorial/)
=======
where `convolutional_network.py` is the tensorflow program to execute while the remainder are arguments to the program.  Program arguments `--trainImagesFile train-images-idx3-ubyte.gz`, `--trainLabelsFile train-labels-idx1-ubyte.gz`, `--testImagesFile t10k-images-idx3-ubyte.gz`, `--testLabelsFile t10k-labels-idx1-ubyte.gz` values refer to the dataset paths in the objectstore container `tf_training_data`. Program arguments `--trainingIters 20000` and `--learningRate 0.001` pass the values of hyperparameters.
**Note**: If the user's model and manifest files refer to some training data, they shouldn't use absolute paths. They should be specified relative to the environment variable `${DATA_DIR}` as in the command above. **Note**: convolutional_network.py should be included in the model zip file that forms the experiment referenced by the url defined in `model_definition.definition_location`## Submitting the training job

Once you have created a training definition file, you can start a training job by POSTing to the WML /v3/models endpoint.  For example, if the training definition is in file training_definition.json and a WML authorisation token is stored in environment variable `$TOKEN`, the following curl command could be used:

```
curl -X POST -sS -H "Content-Type: application/json"  
   -H "Authorization: BEARER ${TOKEN}" 
   -H "X-WML-User-Client: WML-User"  
   --data-binary "@training_definition.json" 
   "https://ibm-watson-ml.stage1.mybluemix.net/v3/models"
```
## Model deployment and trainingAfter creating the manifest file and model zip file refer to instructions under Using deep learning via Bluemix for working with your model in deep learning.
>>>>>>> origin/staging
