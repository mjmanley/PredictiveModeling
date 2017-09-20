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

# Sistema di apprendimento continuo <span class='tag--beta'>Beta</span>

Il sistema di apprendimento continuo fornisce il monitoraggio automatizzato delle prestazioni, del riaggiornamento e della ridistribuzione del modello per garantire la qualità delle previsioni.


**Nome scenario**: Selezione dei farmaci migliori per il trattamento di disfunzioni cardiache.

**Descrizione scenario**: una società biomedica che produce farmaci per il cuore
vuole distribuire un modello che selezioni il farmaco migliore per il trattamento di disfunzioni cardiache. Quando emergono nuove prove sull'efficacia del farmaco, è opportuno prendere in considerazione un aggiornamento del modello. Un data scientist ha preparato
un modello predittivo e lo condivide con te (lo sviluppatore). Il tuo compito è quello di distribuire il modello, impostare la configurazione di apprendimento ed eseguire l'iterazione di apprendimento per valutare, riaggiornare e ridistribuire il modello.

**Nota**: puoi anche utilizzare il  [blocco appunti](https://apsportal.ibm.com/analytics/notebooks/a97cde0b-5bb8-436a-ae82-83e96adc45e0/view?access_token=6baf4c722e452836f7b505205bc96d9a24b9333ee9b5c39453f6d7751987f798) python di esempio che crea un modello di esempio, configura il sistema di apprendimento e infine esegue l'iterazione di apprendimento.

## Utilizzo del modello di esempio

1. Vai alla scheda **Esempi** del dashboard IBM® Watson™ Machine Learning.

2. Nella sezione **Modelli di esempio**, cerca il tile Selezione di farmaci per il cuore e fai clic sull'icona **Aggiungi modello** (+).

Adesso vedrai il modello di esempio Selezione di farmaci per il cuore nell'elenco di modelli disponibili sulla scheda Modelli.

## Generazione del token di accesso

Genera un token di accesso utilizzando l'utente e la password disponibili
dalla scheda Credenziali del servizio dell'istanza del servizio IBM Watson Machine
Learning.

Esempio di
richiesta:

```
curl --basic --user <username>:<password> https://ibm-watson-ml.mybluemix.net/v3/identity/token
```
{: codeblock}

Esempio di output:

```
{"token":"**********"}
```
{: codeblock}

Utilizza il seguente comando di terminale per assegnare il tuo valore token alla variabile di ambiente token:

```
token="<token_value>"
```
{: codeblock}

## Utilizzo di modelli pubblicati

Utilizza la seguente chiamata API per richiamare i dettagli della tua istanza, ad esempio:

* `url` dei modelli pubblicati
* `url` delle distribuzioni
* informazioni di utilizzo

Esempio di
richiesta:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer  $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}
```
{: codeblock}

Esempio di output:

```
{
   "metadata":{
      "guid":"360c510b-012c-4793-ae3f-063410081c3e",
      "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e",
      "created_at":"2017-08-04T09:15:48.344Z",
      "modified_at":"2017-08-22T08:34:47.759Z"
   },
   "entity":{
      "source":"Bluemix",
      "published_models":{
         "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/published_models"
      },
      "usage":{
         "expiration_date":"2017-09-01T00:00:00.000Z",
         "computation_time":{
            "current":4
         },
         "model_count":{
            "limit":1000,
            "current":2
         },
         "prediction_count":{
            "current":16
         },
         "deployment_count":{
            "limit":1000,
            "current":1
         }
      },
      "plan_id":"0f2a3c2c-456b-40f3-9b19-726d2740b11c",
      "status":"Active",
      "organization_guid":"b0e61605-a82e-4f03-9e9f-2767973c084d",
      "region":"us-south",
      "account":{
         "id":"f52968f3dbbe7b0b53e15743d45e5e90",
         "name":"Umit Cakmak's Account",
         "type":"TRIAL"
      },
      "owner":{
         "ibm_id":"31000292EV",
         "email":"umit.cakmak@pl.ibm.com",
         "user_id":"43e0ee0e-6bfb-48fc-bcd8-d61e40d19253",
         "country_code":"POL",
         "beta_user":true
      },
      "deployments":{
         "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/deployments"
      },
      "space_guid":"4c55eb1c-d6fe-4f0a-9390-35c9a7ecf27a",
      "plan":"standard"
   }
}
```
{: codeblock}


Avendo l'`url` dei **modelli_pubblicati**, utilizza la seguente chiamata API per richiamare i dettagli del modello:

Esempio di
richiesta:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer  $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models
```
{: codeblock}

Esempio di output:

```
{  
   "count":1,
   "resources":[  
      {  
         "metadata":{  
      "guid":"361d0edb-c5c9-4b8c-b353-d968e7dc0b8d",
            "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/published_models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d",
            "created_at":"2017-08-22T08:34:47.597Z",
            "modified_at":"2017-08-22T08:34:47.691Z"
         },
   "entity":{  
      "runtime_environment":"spark-2.0",
            "author":{  

            },
            "name":"Best Heart Drug Selection",
            "label_col":"DRUG",
            "training_data_schema":{  
               "fields":[  
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"AGE"
                     },
                     "type":"integer",
                     "name":"AGE",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"SEX"
                     },
                     "type":"string",
                     "name":"SEX",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"BP"
                     },
                     "type":"string",
                     "name":"BP",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"CHOLESTEROL"
                     },
                     "type":"string",
                     "name":"CHOLESTEROL",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":6,
                        "name":"NA"
                     },
                     "type":"decimal(12,6)",
                     "name":"NA",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":6,
                        "name":"K"
                     },
                     "type":"decimal(13,6)",
                     "name":"K",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"DRUG"
                     },
                     "type":"string",
                     "name":"DRUG",
                     "nullable":true
                  }
               ],
               "type":"struct"
            },
            "latest_version":{  
               "url":"https://ibm-watson-ml.mybluemix.net/v2/artifacts/models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d/versions/8dfe9548-57ec-4768-8d3e-6c1e7e5cdfc3",
               "guid":"8dfe9548-57ec-4768-8d3e-6c1e7e5cdfc3",
               "created_at":"2017-08-22T08:34:47.691Z"
            },
            "model_type":"sparkml-model-2.0",
            "deployments":{  
               "count":0,
               "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/published_models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d/deployments"
            },
            "input_data_schema":{  
               "fields":[  
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"AGE"
                     },
                     "type":"integer",
                     "name":"AGE",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"SEX"
                     },
                     "type":"string",
                     "name":"SEX",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"BP"
                     },
                     "type":"string",
                     "name":"BP",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"CHOLESTEROL"
                     },
                     "type":"string",
                     "name":"CHOLESTEROL",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":6,
                        "name":"NA"
                     },
                     "type":"decimal(12,6)",
                     "name":"NA",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":6,
                        "name":"K"
                     },
                     "type":"decimal(13,6)",
                     "name":"K",
                     "nullable":true
                  }
               ],
               "type":"struct"
            }
         }
      }
}
```
{: codeblock}


## Imposta il sistema di apprendimento continuo per il modello pubblicato

In questa sottosezione imparerai a configurare il sistema di apprendimento continuo per il tuo modello.

### Prepara l'intestazione di autorizzazione

Per preparare l'intestazione di autorizzazione che unisce il token di Watson Machine Learning e le credenziali dell'istanza Spark, fornisci i seguenti dettagli:

*  Il token di accesso creato nel passo precedente
*  Le credenziali del servizio Spark, che è possibile trovare nella scheda Credenziali del
   servizio del dashboard del servizio Bluemix Spark. Prima di effettuare la richiesta di distribuzione, le credenziali Spark devono essere codificate in base64. Queste vengono passate nell'intestazione della richiesta nel campo X-Spark-Service-Instance.

   A seconda del sistema operativo che stai utilizzando, devi immettere uno dei seguenti comandi di terminale per eseguire la codifica in base64 e assegnarlo alla variabile di ambiente.

   Sul sistema operativo macOS, utilizza il seguente comando:

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64)
   ```
   {: codeblock}

   Sui sistemi operativi Microsoft Windows o Linux, per eseguire la codifica in base64 devi utilizzare il parametro `--wrap=0` con il comando `base64`:

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64 --wrap=0)
   ```
   {: codeblock}


### Prepara il dataset di feedback

Il sistema di apprendimento richiede la connessione ai dati di formazione (i dati utilizzati nella formazione del modello) e ai dati di feedback (i dati che verranno utilizzati per valutare il modello formato). Utilizza la seguente istruzione per preparare la tabella  **DRUG_FEEDBACK_DATA** in **Db2 Warehouse on Cloud**.

- Crea un'istanza del [Servizio Db2 Warehouse on Cloud](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/) (viene offerto un piano di ingresso).
- Crea la tabella **DRUG_FEEDBACK_DATA** in **Db2 Warehouse on Cloud**.
  + Scarica il file [drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv) dal repository git.
  + Fai clic sull'icona **Apri la console** per iniziare a utilizzare **Db2 Warehouse on Cloud**.
  + Seleziona il tipo di caricamento **Carica dati** e **Desktop**.
  + **Trascina e rilascia** il file precedentemente scaricato e fai clic su **Avanti**.
  + Seleziona **Schema** per importare i dati e fai clic su **Nuova tabella**.
  + Immetti un nome nel campo **nuova tabella** e fai clic su **Avanti**.
  + Per il **separatore campi**, utilizza un punto e virgola (;).
  + Fai clic su **Avanti** per creare la tabella con i dati caricati.

**Nota**: puoi aggiungere nuovi record di feedback al database di feedback utilizzando questo [endpoint API REST](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback)

### Prepara il payload di configurazione

Per specificare la configurazione di apprendimento, devi utilizzare il seguente endpoint:

```
https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_configuration
```
   {: codeblock}


Definisci i valori dei seguenti campi per finalizzare il payload:

* `min_feedback_data_size` - questo è il numero minimo di record nel dataset di feedback per avviare l'iterazione del sistema di apprendimento continuo
* `auto_retrain` [never, always, conditionally] - questo parametro specifica quando deve essere attivato il processo di riaggiornamento. [conditionally] attiverà il processo di riaggiornamento quando la qualità del modello è inferiore alla soglia specificata. 
* `auto_redeploy` [never, always, conditionally] - questo parametro specifica quando deve essere distribuito il modello riaggiornato. [conditionally] attiverà la ridistribuzione del modello quando la qualità del modello appena formato è superiore rispetto a quello attualmente distribuito.


Esempio di
richiesta:

```
curl -v -X PUT \
    -H "Content-Type:application/json" \
    -H "Authorization: Bearer $token" \
    -H "X-Spark-Service-Instance: $spark_credentials" \
    -d '{
          "definition": {
            "method": "binary",
            "metrics": [
              {
                "name": "areaUnderROC",
        "threshold": 0.8
      }
            ]
          },
          "feedback_data_ref": {
           "connection":{
            "db": "BLUDB",
            "host": "awh-yp-small02.services.dal.bluemix.net",
            "username": "dash102204",
            "password": "NweTlYwPY6cu"
           },
    "source": {
            "tablename": "DRUG_FEEDBACK_DATA",
            "type": "dashdb"
           }
          },
          "min_feedback_data_size": 100,
          "auto_retrain": "conditionally",
          "auto_redeploy": "conditionally",
          "schedule": {
            "expression": "0/15 * * * * ? *",
            "start": "2017-02-01T10:11:12Z",
            "until": "2017-06-01T10:11:12Z"
          },
          "last_training_record": 0
        }' \
    https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_configuration
```

{: codeblock}

Esempio di output:
```
{
   "min_feedback_data_size":100,
   "auto_retrain":"conditionally",
   "schedule":{
      "expression":"0/15 * * * * ? *",
      "start":"2017-02-01T10:11:12Z",
      "until":"2017-06-01T10:11:12Z"
   },
   "definition":{
      "method":"binary",
      "metrics":[
         {
            "name": "areaUnderROC",
        "threshold": 0.8
      }
      ]
   },
      "spark_service":{
      "credentials": {
         "tenant_id":"s971-2eeb9ffe2a3090-35c9a7ecf27a",
         "cluster_master_url":"https://spark.bluemix.net",
         "tenant_id_full":"55f1492d-b385-4fdd-b971-2eeb9ffe2a30_4c55eb1c-d6fe-4f0a-9390-35c9a7ecf27a",
         "tenant_secret":"5e7fc568-e94e-4689-b623-fe62e9ceedd2",
         "instance_id":"55f1492d-b385-4fdd-b971-2eeb9ffe2a30",
         "plan":"ibm.SparkService.PayGoPersonal"
      },
         "version":"2.0"
   },
   "feedback_data_ref":{
      "connection":{
         "db":"BLUDB",
         "host":"awh-yp-small02.services.dal.bluemix.net",
         "username":"dash102204",
         "password":"NweTlYwPY6cu"
      },
      "source":{
         "tablename":"DRUG_FEEDBACK_DATA",
         "type":"dashdb"
      }
   },
   "auto_redeploy":"conditionally"
}
```
{: codeblock}

**Nota**: in questo esempio utilizziamo i valori predefiniti per i parametri `auto_retrain` e `auto_redeploy`. Ulteriori informazioni su questi parametri possono essere trovati qui nella [documentazione dell'API REST](http://watson-ml-api.mybluemix.net/#!/Published32Models/put_v3_wml_instances_instance_id_published_models_published_model_id_learning_configuration) per il parametro `learning_configuration`.

## Esegui l'iterazione del sistema di apprendimento continuo

Per avviare l'iterazione del sistema di apprendimento, utilizza il metodo API REST mostrato di seguito. Nell'iterazione, verrà valutato il modello pubblicato. Se l'accuratezza valutata è al di sotto della soglia specificata, verrà attivato il riaggiornamento del modello. Per il riaggiornamento e la valutazione, vengono utilizzati entrambi i dataset: formazione e feedback.

Esempio di
richiesta:

```
curl -X POST --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

Esempio di output:

```
The request has been fulfilled and resulted in a new resource being created.
```
{: codeblock}

Per controllare lo stato dell'iterazione, immetti la seguente richiesta:

Esempio di
richiesta:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

Esempio di output:

```
{
   "count":1,
   "resources":[
      {
         "metadata":{
            "guid":"4091f245-0f0b-42c6-aec9-6ab68185c47f",
            "url":"https://ibm-watson-ml-dev.stage1.mybluemix.net/v3/wml_instances/87452a37-6a8f-4d59-bf88-59c66b5463e4/published_models/9894c3d5-e923-4544-9a7c-2fdb3e4d0908/learning_iterations/4091f245-0f0b-42c6-aec9-6ab68185c47f",
            "created_at":"2017-07-07T11:18:46.742Z",
            "modified_at":"2017-07-07T11:18:48.100Z"
         },
   "entity":{
            "stage":"StartingKernel",
            "published_model":{
               "url":"https://ibm-watson-ml-dev.stage1.mybluemix.net/v3/wml_instances/87452a37-6a8f-4d59-bf88-59c66b5463e4/published_models/9894c3d5-e923-4544-9a7c-2fdb3e4d0908",
               "guid":"9894c3d5-e923-4544-9a7c-2fdb3e4d0908"
            },
            "status":"RUNNING",
            "kernel_id":"db56fc3b-a200-4455-aa70-392aa8ae98b3",
            "spark_service":{
               "credentials": {
                  "tenant_id":"s702-faa29053b44952-01f17dcd4c8c",
                  "cluster_master_url":"https://spark.stage1.bluemix.net",
                  "tenant_id_full":"81d716eb-3c8c-40ef-9702-faa29053b449_a2485898-8ed5-43df-8352-01f17dcd4c8c",
                  "tenant_secret":"9f18945c-8e4b-4d2b-8104-f429b27a896d",
                  "instance_id":"81d716eb-3c8c-40ef-9702-faa29053b449",
                  "plan":"ibm.SparkService.PayGoPersonal"
               }, "version": "2.0"}
         }
      },
   ]
}
```
{: codeblock}

Puoi anche ottenere l'elenco delle metriche e dei valori di valutazione immettendo la seguente richiesta:

Esempio di
richiesta:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/evaluation_metrics
```
{: codeblock}

Esempio di output:

```
{
  "count": 1,
  "resources": [
    {
      "phase": "training",
      "values": [
        {
          "name": "areaUnderROC",
          "value": 0.94,
          "threshold": 0.8
        }
      ],
      "timestamp": "2017-08-08T10:11:12.000Z",
      "artifactVersionHref": "https://ibm-watson-ml.mybluemix.net/v3/artifacts/models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d/versions/8dfe9548-57ec-4768-8d3e-6c1e7e5cdfc3"
    }
  ]
}
```
{: codeblock}
