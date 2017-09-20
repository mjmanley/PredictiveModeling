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

# Introduzione a Watson Machine Learning
{: #WMLgettingstarted}

Utilizza IBM® Watson™ Machine Learning per integrare l'analisi predittiva con le tue applicazioni. Il machine learning è utilizzato dai data scientist per sviluppare modelli predittivi e dagli sviluppatori per creare applicazioni che effettuano decisioni più mirate, risolvono problemi complicati e migliorano i risultati degli utenti.
{: shortdesc}

## Prerequisiti

Per utilizzare Watson Machine Learning, dal catalogo Bluemix, devi creare l'[istanza del servizio qui](https://console.bluemix.net/catalog/services/ibm-watson-machine-learning/).

## Passi

1. [Crea e memorizza un modello](pm_custom_models.html).
2. [Distribuisci un modello](pm_service_api_spark_online.html).
3. Utilizza il modello distribuito `endpoint di calcolo del punteggio` nella tua applicazione per [generare previsioni.](pm_service_api_spark_building.html)

## Informazioni

Il servizio Watson Machine Learning consiste in un insieme di API REST che possono essere richiamate
da qualsiasi linguaggio di programmazione.

L'obiettivo del servizio Watson Machine Learning è la distribuzione, ma tieni
presente che è necessario IBM SPSS Modeler o Data Science Experience per
la creazione e l'utilizzo di modelli e pipeline. SPSS
Modeler e Data Science Experience (che utilizza Spark MLlib e Python scikit-learn)
offrono entrambi diversi metodi di modellazione derivanti dal machine
learning, dall'intelligenza artificiale e dalle statistiche.

## Link correlati

Sei pronto a iniziare? Per creare un'istanza di un servizio o per eseguire il bind
di un'applicazione, vedi [Utilizzo del servizio con i modelli Spark e Python](using_pm_service_dsx.html) oppure
[Utilizzo del servizio con i modelli SPSS](using_pm_service.html).

Se sei interessato ad esplorare l'API, vedi [API del servizio per i modelli Spark e Python](pm_service_api_spark.html) o [API del
servizio per i modelli SPSS](pm_service_api_spss.html).

Per i dettagli su SPSS Modeler e sugli algoritmi di modellazione che fornisce, consulta [IBM
Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7).

Per i dettagli su IBM Data Science Experience e sugli algoritmi di
modellazione che fornisce, vedi [https://datascience.ibm.com](https://datascience.ibm.com).
