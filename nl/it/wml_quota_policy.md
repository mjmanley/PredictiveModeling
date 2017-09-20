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

# Politica delle quote

Il motore di IBM Watson Machine Learning applica delle quote sulla base di ogni istanza per garantire l'assegnazione e l'utilizzo appropriati delle risorse. Queste politiche variano in base ai profili dell'account, all'uso storico dei servizi e alla disponibilità delle risorse. La politica delle quote descrive i limiti che non sono definiti dal piano dei prezzi e che **sono soggetti a modifiche senza preavviso**. 

Attualmente, sono attivi i seguenti limiti di quota dei servizi.

## Utilizzo delle risorse

Le risorse sono limitate ai seguenti valori massimi:

-  **Numero massimo di modelli pubblicati**: 200 (piano Gratuito) 1000 (piani Standard & Professional)
-  **Dimensione massima del modello Spark ML**: 200 MB
-  **Numero massimo di modelli distribuiti**: 1000 (piani Standard & Professional)

**Nota**: per comprendere i limiti del piano Gratuito, consulta la descrizione del [piano Gratuito](https://console.bluemix.net/catalog/services/machine-learning) nel [catalogo Bluemix](https://console.bluemix.net/catalog/).

## Limiti di richieste del servizio

Esistono dei limiti nel numero di richieste che puoi effettuare al minuto a specifiche API. Se la tua applicazione ha bisogno di limiti superiori, devi [contattare il supporto IBM Bluemix](https://support.ng.bluemix.net/) per aumentare la tua quota.

## Richieste di distribuzione

Alle richieste API di distribuzione si applicano i seguenti limiti:

-  **Periodo**: 60 secondi
-  **Limite predefinito**: 10

## Richieste di previsione online

Alle richieste di [previsioni online](pm_service_api_spark_building.html) si applicano i seguenti limiti:

-  **Periodo**: 60 secondi
-  **Limite predefinito**: 500

## Richieste di gestione risorse

Alle richieste totali combinate in questo elenco si applicano i seguenti limiti:

[Token](https://watson-ml-api.mybluemix.net/#/Token): richieste post, get, delete, put, patch

[Distribuzioni](https://watson-ml-api.mybluemix.net/#/Deployments): richieste post, get, delete, put, patch

-  **Periodo**: 60 secondi
-  **Limite predefinito**: 100
