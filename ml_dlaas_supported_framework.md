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

# Supported deep learning frameworks

You can deploy models based on the supported deep learning frameworks and then train your models on the {{site.data.keyword.pm_full}} infrastructure by leveraging GPUs. You can use the `cURL` command to invoke deep learning APIs through {{site.data.keyword.Bluemix}} or use the deep learning {{site.data.keyword.Bluemix_short}} command line interface plugin.
{: shortdesc}

The {{site.data.keyword.pm_full}} service supports the following deep learning frameworks for training:

* Tensorflow (with Keras 2) versions **1.2-py2**, **1.2-py3**, **1.3-py2**, and **1.3-py3**
* Caffe version **1.0-py2**
* Torch7 built as version **luajit** or **lua52**
* Theano (with Lasagne) version **0.9**
* Caffe2 version **0.7**
* MXNet version **0.10**

## Learn more

[A quick deep learning tutorial](https://www.ibm.com/blogs/watson/2016/10/quick-deep-learning-tutorial/)

<!-- Models trained using the following frameworks can be additionally be deployed (deployment support for other frameworks will be added):

* Tensorflow (with Keras 2) versions **1.2-py3**
-->