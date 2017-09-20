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

# Distribuzione di modelli batch <span class='tag--beta'>Beta</span>

**Nota**: questa funzionalità è attualmente in beta e disponibile solo
per l'utilizzo con Spark MLlib. Se sei interessato a partecipare, inserisci il tuo nome nella lista di attesa. Per ulteriori informazioni, vedi: [https://www.ibm.biz/mlwaitlist](https://www.ibm.biz/mlwaitlist).

**Nome scenario**: Previsione soddisfazione del cliente.

**Descrizione scenario**: una società di telecomunicazioni vuole sapere
quali clienti sono a rischio di abbandono. Il modello presentato prevede l'abbandono dei clienti. Un data scientist
sviluppa un modello predittivo e lo condivide con te (lo sviluppatore). Il tuo compito è quello di distribuire
il modello e di generare l'analisi predittiva effettuando richieste di punteggio sul modello distribuito.

## Utilizzo del modello di esempio

1.  Vai alla scheda Esempi del dashboard IBM® Watson™ Machine
   Learning.

2.  Nella sezione Modelli di esempio, cerca il tile Previsione soddisfazione del
   cliente e fai clic sul pulsante Aggiungi modello (+).

Adesso vedrai il modello di esempio Previsione soddisfazione del cliente
nell'elenco di modelli disponibili sulla scheda Modelli.

## Creazione di una distribuzione batch con Object Storage

1.  Vai alla scheda Modelli del dashboard IBM® Watson™ Machine Learning.

2.  Dal menu **Azioni**, fai clic su **Crea distribuzione**.

3.  Nel modulo Crea distribuzione, fornisci Nome, Descrizione e Tipo batch.

4.  Devi fornire i seguenti input:

    **Connessione di input**: i dettagli di Object Storage, che verranno utilizzati come input (dati cliente per il calcolo del punteggio) per il modello e archiviazione per l'output del modello (in questo caso, results.csv, che viene creato automaticamente).

    ```
       {
          "source":{
             "fileformat":"csv",
      "firstlineheader":"true",
      "container":"batchjob",
      "inferschema":"1",
      "filename":"TelcoCustomerData.csv",
      "type":"bluemixobjectstorage"
          },
          "connection":{
             "projectid":"252341ed707d4558b5b2da245e785cd7",
             "userid":"b2d83cf6056e040ddb91ca00a2686c7d3",
             "region":"dallas",
             "authurl":"https://identity.open.softlayer.com",
             "password":"eJ_y9R^OE{j?8Ub!!"
          }
       }
    ```
    {: codeblock}

    **Connessione di output**

    ```
       {
          "target":{
             "fileformat":"csv",
      "firstlineheader":"true",
      "container":"batchjob",
      "inferschema":"1",
      "filename":"result.csv",
      "type":"bluemixobjectstorage"
          },
          "connection":{
             "projectid":"252341ed707d4558b5b2da245e785cd7",
             "userid":"b2d83cf6056e040ddb91ca00a2686c7d3",
             "region":"dallas",
             "authurl":"https://identity.open.softlayer.com",
             "password":"eJ_y9R^OE{j?8Ub!!"
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

5.  Fai clic su **Salva**.

Il risultato della previsione viene salvato in un file .csv in IBM Object
Storage. Di seguito è riportata una riga di esempio.

Anteprima file di
input:

```
customerID,gender,SeniorCitizen,Partner,Dependents,tenure,PhoneService,MultipleLines,InternetService,OnlineSecurity,OnlineBackup,DeviceProtection,TechSupport,StreamingTV,StreamingMovies,Contract,PaperlessBilling,PaymentMethod,MonthlyCharges,TotalCharges,Churn
7590-VHVEG,Female,0,Yes,No,1,No,No phone service,DSL,No,Yes,No,No,No,No,Month-to-month,Yes,Electronic check,29.85,29.85,No
5575-GNVDE,Male,0,No,No,34,Yes,No,DSL,Yes,No,Yes,No,No,No,One year,No,Mailed check,56.95,1889.5,No
3668-QPYBK,Male,0,No,No,2,Yes,No,DSL,Yes,Yes,No,No,No,No,Month-to-month,Yes,Mailed check,53.85,108.15,Yes
```
{: codeblock}

Anteprima file di output:

```
InternetService, Contract, tenure, MonthlyCharges, Churn
Fiber optic, Month-to-month, 2, 70.7, 1
DSL, Two year, 58, 59.9, 0
DSL, Month-to-month, 1, 30.2, 1
DSL, Month-to-month, 17, 64.7, 1
DSL, Month-to-month, 13, 76.2, 0
DSL, Month-to-month, 25, 69.5, 1
Fiber optic, Month-to-month, 8, 80.65, 1
No, One year, 52, 20.4, 0
Fiber optic, Two year, 64, 111.6, 0
Fiber optic, Month-to-month, 1, 79.35, 1
```
{: codeblock}


## Recupero dei dettagli di distribuzione

Puoi controllare lo stato e i parametri correlati al modello distribuito.

1. Vai alla scheda Distribuzioni del dashboard IBM® Watson™ Machine
   Learning.

2. Dal menu AZIONI, seleziona Visualizza dettagli.


## Eliminazione di una distribuzione batch

Puoi eliminare una distribuzione che non ti serve più utilizzando una query come nel seguente
esempio.

1. Vai alla scheda Distribuzioni del dashboard IBM® Watson™ Machine
   Learning.

2. Dal menu AZIONI, seleziona Elimina.
