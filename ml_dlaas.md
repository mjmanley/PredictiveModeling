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

# Experiment-centric training of neural networks <span class='tag--beta'>(beta)</span>

As a data scientist, you need to train hundreds of models to identify the right combination of data plus hyperparameters that optimizes the performance of your neural networks.  You want to perform more experiments…and faster.  You want to train deeper networks and explore broader hyperparameters spaces. {{site.data.keyword.pm_full}} accelerates this experimental cycle by simplifying the process to train models in parallel on an elastic GPU compute cluster.
{: shortdesc}

Here's how to get started:
1. [Setup your environment for {{site.data.keyword.pm_full}}](ml_getting_access.html)
2. Upload training data to the cloud
3. Configure each training run
4. Start training
5. Monitor and evaluate

<!-- ![deep learning process flow](images/ml_dlaas_api_calls.png) -->

## Upload training data to the cloud

Before you can start training your neural networks, you first need to move your data into the IBM Cloud.  To do this, first create an instance of the [Object Storage Service](ml_dlaas_object_store.html) to host your training data.  Using the visual tooling provided by the Object Storage service, you can drag-and-drop your files directly into your Object Storage instance.  And when you're done training, the output from your training runs will be written to your object store so you can drag-and-drop files back to your desktop if needed.

## Configure each training run

After [setting up your local environment](ml_getting_access.html), you need to [define each of your training runs](ml_dlaas_working_with_new_models.html).  A training run consists of two parts: (1) your neural network model defined using one of the [supported deep learning frameworks](ml_dlaas_supported_framework.html) plus (2) the configuration for how to run your training including the number of GPUs and location of the Object Store containing your dataset.

<p align="center"><img src="images/experiment_to_training_runs_text.png" alt="relation of experiments to training runs"></p>

In {{site.data.keyword.pm_full}}, the organizing unit that tracks your training runs is called an Experiment.  Experiment are groupings of dozens to hundreds of training runs that you've chosen to associate together based on a related neural network model definition or range of hyperparameters being explored.

## Start training

After you’ve created your training definitions, use the [CLI (Command Line Interface)](ml_dlaas_environment.html) to submit your jobs to {{site.data.keyword.pm_full}}. {{site.data.keyword.pm_full}} will package each of your training runs and allocate them to a Kubernetes container with the requested resources and deep learning framework.  Training runs are executed in parallel depending on the GPU resources available to your account level.  For free accounts, your are limited to 1 GPU so all additional runs will be queued.

<p align="center"><img src="images/ml_dlaas_markitecture.png" alt="deep learning process flow"></p>

As indicated in the above "markitecture" diagram, 4 training runs have been allocated to 4 containers.  Each of these containers hosts the deep learning framework required by the training run and has access to a single K40 GPU (in this instance).  All resources are allocated elastically so you'll only be charged from the time your training run is assigned a GPU until the training completed and output data is transferred to your Object Storage instance.

## Next Steps

Get started using these [sample training runs](ml_dlaas_working_with_sample_models.html) or create your own [new training runs](ml_dlaas_working_with_new_models.html).
