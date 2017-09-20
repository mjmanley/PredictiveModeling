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

# Distribuzione di modelli streaming <span class='tag--beta'>Beta</span>

**Nota**: questa funzionalità è attualmente in beta e disponibile solo
per l'utilizzo con Spark MLlib. Se sei interessato a partecipare, inserisci il tuo nome nella lista di attesa. Per ulteriori informazioni, vedi: [https://www.ibm.biz/mlwaitlist](https://www.ibm.biz/mlwaitlist).

**Nome scenario**: Analisi delle valutazioni.

**Descrizione scenario**: un'agenzia di marketing vuole conoscere le
valutazioni in merito a un determinato argomento. L'agenzia ci richiede di
sviluppare un modello che classifichi una data istruzione come POSITIVA o
NEGATIVA. Un data scientist prepara un modello predittivo e lo condivide con te (lo sviluppatore). Il tuo compito è quello di distribuire
il modello e di generare l'analisi predittiva effettuando richieste di punteggio sul modello distribuito.

Per ulteriori informazioni, vedi questo [documento](https://github.com/pmservice/tweet-sentiment-prediction).

## Utilizzo del modello di esempio

1. Vai alla scheda Esempi del dashboard IBM® Watson™ Machine
   Learning.
2. Nella sezione Modelli di esempio, cerca il tile Previsione
   valutazioni e fai clic sul pulsante Aggiungi modello (+).

Adesso vedrai il modello di esempio Previsione valutazioni nell'elenco di
modelli disponibili sulla scheda Modelli.


## Creazione di una distribuzione streaming con IBM Message Hub

1.  Vai alla scheda Modelli del dashboard IBM® Watson™ Machine Learning.
2.  Dal menu AZIONI, seleziona Crea distribuzione.
3.  Nel modulo Crea distribuzione, fornisci Nome, Descrizione e Tipo stream.
4.  Devi fornire i seguenti input:

    **Connessione di input**: i dettagli degli argomenti di IBM Message Hub che verranno utilizzati come input (tweet) per il modello e archiviazione per l'output del modello  (risultati della previsione).

    ```
  {
     "connection":{
        "kafka_brokers_sasl":[
           "kafka01-prod01.messagehub.services.us-south.bluemix.net:9093",
         "kafka02-prod01.messagehub.services.us-south.bluemix.net:9093",
         "kafka03-prod01.messagehub.services.us-south.bluemix.net:9093",
         "kafka04-prod01.messagehub.services.us-south.bluemix.net:9093",
         "kafka05-prod01.messagehub.services.us-south.bluemix.net:9093"
        ],
      "kafka_admin_url":"https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443",
      "api_key":"Dv5kEVNNsbuJ9RFEKdUhIn2hruipIrsBolge6v1uQmTzEQti",
      "mqlight_lookup_url":"https://mqlight-lookup-prod01.messagehub.services.us-south.bluemix.net/Lookup?serviceId=5448397d-cb22-4698-8a2b-ffb04f43a4cb",
      "kafka_rest_url":"https://kafka-rest-prod01.messagehub.services.us-south.bluemix.net:443",
      "user":"Dv5kEVNNsbuJ9RFE",
      "password":"KdahIn2hruipIrsBolge6v1uQmTzEQti"
     },
   "source":{
        "topic":"sinput",
         "type":"kafka"
      }
  }
    ```
    {: codeblock}

    **Connessione di output**

    ```
 {
    "connection":{
       "kafka_brokers_sasl":[
          "kafka01-prod01.messagehub.services.us-south.bluemix.net:9093",
         "kafka02-prod01.messagehub.services.us-south.bluemix.net:9093",
         "kafka03-prod01.messagehub.services.us-south.bluemix.net:9093",
         "kafka04-prod01.messagehub.services.us-south.bluemix.net:9093",
         "kafka05-prod01.messagehub.services.us-south.bluemix.net:9093"
       ],
      "kafka_admin_url":"https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443",
      "api_key":"Dv5kEVNNsbuJ9RFEKdUhIn2hruipIrsBolge6v1uQmTzEQti",
      "mqlight_lookup_url":"https://mqlight-lookup-prod01.messagehub.services.us-south.bluemix.net/Lookup?serviceId=5448397d-cb22-4698-8a2b-ffb04f43a4cb",
      "kafka_rest_url":"https://kafka-rest-prod01.messagehub.services.us-south.bluemix.net:443",
      "user":"Dv5kEVNNsbuJ9RFE",
      "password":"KdahIn2hruipIrsBolge6v1uQmTzEQti"
    },
   "target":{
       "topic":"soutput",
         "type":"kafka"
      }
 }
    ```
    {: codeblock}

    **Connessione Spark**: le credenziali del servizio Spark possono essere trovate nella scheda Credenziali del servizio del dashboard del servizio Bluemix Spark.

     ```
{
     "credentials": {
       "tenant_id": "s745-299dcf850a6390-35c9a7ecf27a",  
      "tenant_id_full": "ba3dde5a-ee64-4057-9749-299dcf850a63_4c55eb1c-d6fe-4f0a-9390-35c9a7ecf27a",  
      "cluster_master_url": "https://spark.bluemix.net",  
      "instance_id": "ba3dde5a-ee64-4057-9749-299dcf850a63",  
      "tenant_secret": "c0cba7a4-7b19-46e6-9326-44c4f48aaf08",  
      "plan": "ibm.SparkService.PayGoPersonal"
     },
         "version":"2.0"
}
     ```
     {: codeblock}

5. Fai clic su **Salva**.

Il risultato della previsione viene inviato all'argomento MessageHub definito (connessione di output).

## Recupero dei dettagli di distribuzione

Puoi controllare lo stato e i parametri correlati al modello distribuito.

1. Vai alla scheda Distribuzioni del dashboard IBM® Watson™ Machine
   Learning.
2. Dal menu **Azioni**, fai clic su **Visualizza dettagli**.

## Eliminazione di una distribuzione streaming

Puoi eliminare una distribuzione che non ti serve più utilizzando una query come nel seguente
esempio.

1. Vai alla scheda Distribuzioni del dashboard IBM® Watson™ Machine
   Learning.
2. Dal menu AZIONI, seleziona Elimina.
