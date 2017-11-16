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

# Installing the Command line interface (CLI)

To conduct deep learning experiments using {{site.data.keyword.pm_full}}, first [set up your environment](ml_getting_access.html) then install the command line interface (CLI) which support creating and monitoring training runs.
{: shortdesc}

## Install the command line interface

1.  Install the [command line interface](http://clis.ng.bluemix.net/ui/home.html), which as its instructions explain pre-reqs installing the [CLI](https://console.stage1.ng.bluemix.net/docs/starters/install_cli.html)
2.  Download a version of the CLI plugin from the [ML CLI releases](https://github.ibm.com/NGP-TWC/wml-cli/releases) page of this repository. Be sure to get the right version for your platform.
3. Install CLI plugin (for example on OSX this downloaded as ml_cli_plugin_osx)

   ```
   bx plugin install ml_cli_plugin_osx
   ```
   {: codeblock}

   Sample output:

   ```
   Installing binary...
   OK
   Plug-in 'machine-learning 1.0.0' was successfully installed into /Users/username/.bluemix/plugins/machine-learning. Use 'bx plugin show machine-learning' to show its details.
   ```

4.  Verify the CLI plugin is installed

   ```
   bx ml help
   ```
   {: codeblock}

Sample output:

```
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
   help      Enter 'bx ml help [command]' for more information about a command.
```
{: codeblock}

## Configure the CLI with your environment info

To use the CLI's other commands, you need to set a few environment variables in your operating system.  If you are working in Linux, then run the commands below while replacing the values for ML_USERNAME and ML_PASSWORD with your credentials. You can get the values needed below by following the [directions to  retrieve your  access credentials](ml_getting_access.html#retrieving-your-credentials) to you instance of  {{site.data.keyword.pm_full}}.  

```
export ML_INSTANCE=7da52fac-a4c7-43bf-b7f2-824e5ecd672d
export ML_USERNAME=0e8533a2-81d1-4675-9230-3c9f841s8d57
export ML_PASSWORD=63342b04-27fe-42b9-8b70-ef454dddc0c2
```

## Start a model training run

You're now ready to [create and start your training runs](ml_dlaas_working_with_new_models.html) using the CLI.  Or you can [start by training an example neural network model](ml_dlaas_working_with_sample_models.html) if you want to learn a few of our recommended best practices.

### CLI Upgrade

Check [ML CLI releases](https://github.ibm.com/NGP-TWC/wml-cli/releases) for new versions of the ML CLI. We encourage you to download the latest release of CLI to have the most up-to date features. After downloading
the latest version of ML CLI for your operating system, you need to uninstall the plugin (if you already have an older
version installed) and then install the new version.

```
bluemix plugin uninstall "machine-learning"
```
{: codeblock}

Sample output:

```
Uninstalling plug-in 'deep-learning'...
Uninstalling plug-in 'machine-learning'...
OK
Plug-in 'machine-learning' was successfully uninstalled.
```

Install the new version by running the following command:

```
bluemix plugin install ml_cli_plugin_osx
```
{: codeblock}

Sample output:

```
Installing binary...
OK
Plug-in 'machine-learning 1.0.1' was successfully installed into /Users/username/.bluemix/plugins/machine-learning. Use 'bx plugin show machine-learning' to show its details.
```
{: codeblock}
