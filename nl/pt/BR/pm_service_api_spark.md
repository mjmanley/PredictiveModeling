---

copyright:
  years: 2016, 2017
lastupdated: "2017-09-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API de serviço


O serviço do Machine Learning é um conjunto de APIs de REST que são chamadas por meio de qualquer
linguagem de programação, permitindo a integração da analítica desenvolvida do Data Science Experience
em seus aplicativos. Ligue seus
aplicativos Bluemix à instância de serviço de Machine Learning e
gere as análises preditivas que seus aplicativos precisam para
entregar maior valor a seus usuários. Gerencie modelos no [painel de
administração](pm_service_ui_spark.html) e use o painel para criar implementações on-line, em lote ou de fluxo integradas com seus
aplicativos.

Desenvolva aplicativos nos arquivos do Data Science Experience
(modelos Spark e Python) que sejam implementados em uma instância de serviço
por meio de poderosas [APIs de REST](https://watson-ml-api.mybluemix.net/):

*  Recupere os metadados para um determinado modelo preditivo
*  Implemente modelos e gerencie modelos implementados
    *  Implementação on-line (pontuação)
    *  Implementação em lote (suporta o Db2 Warehouse on Cloud)
    *  Implementação de fluxo (suporte ao IBM MessageHub)
*  Recupere os metadados para uma determinada implementação
*  Gere análise preditiva fazendo solicitações de pontuação em
modelos implementados

Consulte as seções a seguir para obter exemplos de uso da API de REST:

*  [Implementação e pontuação on-line](pm_service_api_spark_online.html)
*  [Implementação em lote com o Db2 Warehouse on
Cloud](pm_service_api_spark_batch.html)
*  [Implementação de fluxo com MessageHub](pm_service_api_spark_streaming.html)
