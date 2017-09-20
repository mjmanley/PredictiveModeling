---

copyright:
  years: 2016, 2017
lastupdated: "2017-09-07"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introdução ao Watson Machine Learning
{: #WMLgettingstarted}

Use o IBM® Watson™ Machine Learning para integrar a analítica preditiva aos seus aplicativos. Os cientistas de dados usam aprendizado por máquina para desenvolver modelos preditivos, ao passo que os desenvolvedores usam aprendizado por máquina para criar aplicativos que tomam decisões mais inteligentes, resolvem problemas difíceis e melhoram os resultados do usuário.
{: shortdesc}

## Pré-requisitos

Para usar o Watson Machine Learning, no catálogo do Bluemix, deve-se criar a [instância de serviço aqui](https://console.bluemix.net/catalog/services/ibm-watson-machine-learning/).

## Etapas

1. [Criar e armazenar um modelo](pm_custom_models.html).
2. [Implementar um modelo](pm_service_api_spark_online.html).
3. Use o `scoring endpoint` do modelo implementado em seu aplicativo para [obter predições.](pm_service_api_spark_building.html)

## Sobre

O serviço do Watson Machine Learning é um conjunto de APIs de REST que podem ser chamadas por meio de
qualquer linguagem de programação.

O foco do serviço do Watson Machine Learning é a implementação,
mas observe que o IBM SPSS Modeler ou o Data Science Experience é necessário para criar
e trabalhar com modelos e pipelines. O SPSS
Modeler e o Data Science Experience (aproveitando o scikit-learn do Spark MLlib e Python) oferecem vários métodos de modelagem que são extraídos do aprendizado de
máquina, inteligência artificial e estatísticas.

## Links relacionados

Pronto para começar? Para criar uma instância de um serviço ou ligar
um aplicativo, veja [Usando o serviço com modelos Spark e Python](using_pm_service_dsx.html) ou
[Usando o serviço com modelos SPSS](using_pm_service.html).

Se estiver interessado em explorar a API, consulte [API de serviço para modelos Spark e Python](pm_service_api_spark.html) ou [API
de serviço para modelos SPSS](pm_service_api_spss.html).

Para obter detalhes sobre o SPSS Modeler e a modelagem de algoritmos que ele
fornece, consulte o [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7).

Para obter detalhes sobre o IBM Data Science Experience e os algoritmos de
modelagem que ele fornece, veja [https://datascience.ibm.com](https://datascience.ibm.com).
