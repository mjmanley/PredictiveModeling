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

# Supported frameworks

The service provides support for a number of different deep learning frameworks at particular versions of the libraries, allowing you a wide range of choices for your deep learning project.
{: shortdesc}

## Listing supported deep learning frameworks

To get an up to date list of framework (names and versions) using the [command line interface](ml_dlaas_environment.html) using the command ```bx ml list frameworks```

```
bx ml list frameworks
```
{: codeblock}

Sample output:

```
Fetching the list of frameworks ...
SI No   Name           Version
1       scikit-learn   0.17
2       tensorflow     1.2-py2
3       tensorflow     1.2-py3
4       tensorflow     1.3-py2
5       tensorflow     1.3-py3
6       caffe          1.0-py2
7       torch          luajit
8       torch          lua52
9       mxnet          0.10
10     theano         0.10
11     caffe2         0.8
OK
List frameworks successful
```

**Note**: where the framework is programmed using the python language, the version should have a ```-py2``` or ```-py3``` extension to indicate whether python2 or python3 should be used.

<!-- Models trained using the following frameworks can be additionally be deployed (deployment support for other frameworks will be added):

* Tensorflow (with Keras 2) versions **1.2-py3**
-->
