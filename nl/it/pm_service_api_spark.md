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

# API del servizio


Il servizio Machine Learning  consiste in un insieme di API REST richiamate
da qualsiasi linguaggio di programmazione, il che permette l'integrazione dell'analisi sviluppata da Data Science
Experience nelle tue applicazioni. Esegui il bind delle tue
applicazioni Bluemix all'istanza del servizio Machine Learning e
genera l'analisi predittiva di cui hanno bisogno le tue applicazioni
per offrire un valore più elevato ai tuoi utenti. Gestisci i modelli nel
[dashboard di amministrazione](pm_service_ui_spark.html) e utilizza il dashboard per creare distribuzioni online,
batch o streaming integrate con le tue
applicazioni.

Sviluppa le applicazioni nei file Data Science Experience
(modelli Spark e Python) che vengono distribuiti su un'istanza del servizio
attraverso le potenti [API REST](https://watson-ml-api.mybluemix.net/):

*  Richiama i metadati per uno specifico modello predittivo
*  Distribuisci i modelli e gestisci i modelli distribuiti
    *  Distribuzione online (punteggio)
    *  Distribuzione batch (supporta Db2 Warehouse on Cloud)
    *  Distribuzione streaming (supporta IBM MessageHub)
*  Richiama i metadati per una specifica distribuzione
*  Genera l'analisi predittiva effettuando richieste di punteggio sui modelli distribuiti

Vedi le seguenti sezioni per degli esempi di utilizzo dell'API REST:

*  [Distribuzione online e punteggio](pm_service_api_spark_online.html)
*  [Distribuzione batch con Db2 Warehouse on Cloud](pm_service_api_spark_batch.html)
*  [Distribuzione streaming con MessageHub](pm_service_api_spark_streaming.html)
