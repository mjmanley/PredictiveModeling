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

# Fortlaufendes Ausbildungssystem <span class='tag--beta'>Beta</span>

Das fortlaufende Ausbildungssystem bietet eine automatisierte Überwachung des Modellerfolgs, erneutes Training und erneute Bereitstellung zur Sicherung der Vorhersagequalität. 


**Szenarioname**: Beste Auswahl für ein Medikament zur Herzbehandlung.

**Szenariobeschreibung**: Ein Biomedizinisches Unternehmen, das Herzmedikamente herstellt, möchte ein Modell bereitstellen, das das jeweils beste Medikament für die Herzbehandlung auswählt. Wenn neue Nachweise zur Wirksamkeit des Medikaments auftauchen, sollte eine Modellaktualisierung in Erwägung gezogen werden. Ein Data-Scientist entwickelt ein Vorhersagemodell und
teilt es mit Ihnen (dem Entwickler). Ihre Aufgabe ist es, das Modell bereitzustellen, die Konfiguration für die Schulung zu definieren und eine Lernwiederholung durchzuführen, um das Modell zu evaluieren, erneut zu trainieren und erneut bereitzustellen. 

**Hinweis**: Sie können mit dem Pyhton-Beispiel für das [Notizbuch](https://apsportal.ibm.com/analytics/notebooks/a97cde0b-5bb8-436a-ae82-83e96adc45e0/view?access_token=6baf4c722e452836f7b505205bc96d9a24b9333ee9b5c39453f6d7751987f798), das ein Beispielmodell erstellt, ein Ausbildungssystem konfiguriert und schließlich eine Lernwiederholung durchführt auch spielerisch umgehen. 

## Beispielmodell verwenden

1. Wechseln Sie zur Registerkarte **Beispiele** des IBM® Watson™ Machine Learning Dashboards.

2. Suchen Sie im Abschnitt **Beispielmodelle** das Beispiel mit der Kachel 'Heart Drug Selection'
   und klicken Sie auf das Symbol **Modell hinzufügen** (+).

Das Modell für die Auswahl des Herzmedikaments wird in der Liste der verfügbaren Modelle auf der Registerkarte 'Modelle' angezeigt. 

## Zugriffstoken generieren

Generieren Sie mithilfe des Benutzers und des Kennworts, die auf der Registerkarte
Serviceberechtigungsnachweise der IBM Watson Machine Learning-Serviceinstanz
angegeben sind, ein Zugriffstoken (access token).

Anforderungsbeispiel:

```
curl --basic --user <username>:<password> https://ibm-watson-ml.mybluemix.net/v3/identity/token
```
{: codeblock}

Ausgabebeispiel:

```
{"token":"**********"}
```
{: codeblock}

Verwenden Sie den folgenden Terminalbefehl, um Ihren Tokenwert dem
Umgebungsvariablentoken zuzuweisen: 

```
token="<token_value>"
```
{: codeblock}

## Mit veröffentlichten Modellen arbeiten

Verwenden Sie den folgenden API-Aufruf, um Ihre Instanzdetails abzurufen. Zum Beispiel: 

* Veröffentlichte Modelle `URL`
* Bereitstellungen `URL`
* Nutzungsinformationen

Anforderungsbeispiel:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer  $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}
```
{: codeblock}

Ausgabebeispiel:

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


Verwenden Sie bei der URL von veröffentlichten Modellen (**published_models** `url`) den folgenden API-Aufruf, um Modelldetails abzurufen: 

Anforderungsbeispiel:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer  $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models
```
{: codeblock}

Ausgabebeispiel:

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


## Fortlaufendes Ausbildungssystem für das veröffentlichte Modell festlegen

In diesem Unterabschnitt lernen Sie, wie ein fortlaufendes Ausbildungssystem für Ihr Modell konfiguriert wird. 

### Berechtigungsheader vorbereiten

Stellen Sie folgende Details zur Verfügung, um den Berechtigungsheader vorzubereiten, der das Watson Machine Learning-Token und die Spark-Instanzberechtigungsnachweise kombiniert. 

*  Das im vorherigen Schritt erstellte Zugriffstoken
*  Spark-Serviceberechtigungsnachweise, die Sie auf der Registerkarte
Serviceberechtigungsnachweise des Bluemix Spark-Servicedashboards finden. Bevor die
Bereitstellungsanforderung gestellt werden kann, müssen Spark-Berechtigungsnachweise
als Base64 codiert werden. Sie werden im Header der Anforderung im Feld X-Spark-Serviceinstanz übergeben. 

   Setzen Sie abhängig vom verwendeten Betriebssystem einen der folgenden Terminalbefehle ab, um die Base64-Codierung auszuführen, und weisen Sie ihn der Umgebungsvariablen zu. 

   Verwenden Sie unter dem Betriebssystem macOS den folgenden Befehl:

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64)
   ```
   {: codeblock}

   Verwenden Sie unter den Betriebssystemen Microsoft Windows und Linux den Parameter `--wrap=0` im Befehl `base64`, um die
Base64-Codierung auszuführen: 

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64 --wrap=0)
   ```
   {: codeblock}


### Feedbackdatei vorbereiten 

Das Ausbildungssystem erfordert eine Verbindung zu den Trainingsdaten (Daten, die im Modelltraining verwendet wurden) sowie zu den Feedbackdaten (Daten, die zur Evaluierung des Trainingsmodells verwendet wurden). Befolgen Sie die unten aufgeführte Anweisung, um die Tabelle **DRUG_FEEDBACK_DATA** in der **Db2 Warehouse on Cloud** vorzubereiten.

- Erstellen Sie eine Instanz von [Db2 Warehouse on Cloud Service](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/) (ein Eingabeplan wird angeboten). 
- Erstellen Sie die Tabelle **DRUG_FEEDBACK_DATA** in **Db2 Warehouse on Cloud**.
  + Laden Sie die Datei [drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv) vom git-Repository herunter
  + Klicken Sie auf **Konsole öffnen**, um mit dem Symbol **Db2 Warehouse on Cloud** zu beginnen. 
  + Wählen Sie die Option **Daten laden** und den Ladetyp **Desktop** aus. 
  + Wählen Sie für die zuvor heruntergeladene Datei **Ziehen und Ablegen** aus und klicken Sie auf **Weiter**.
  + Wählen Sie **Schema** aus, um Daten zu importieren und klicken Sie auf **Neue Tabelle**.
  + Geben Sie im Feld **Neue Tabelle** einen Namen an und klicken Sie auf **Weiter**.
  + Verwenden Sie als **Feldtrennzeichen** ein Semikolon (;).
  + Klicken Sie auf **Weiter**, um eine Tabelle mit den hochgeladenen Daten zu erstellen. 

**Hinweis**: Sie können neue Feedbackdatensätze zur Feedbackdatenbank hinzufügen, indem Sie diesen [REST-API-Endpunkt](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback) verwenden.

### Konfigurationsnutzdaten vorbereiten

Sie müssen folgenden Endpunkt verwenden, um eine Lernkonfiguration anzugeben:

```
https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_configuration
```
   {: codeblock}


Definieren Sie die Werte der folgenden Felder, um die Vorbereitung der Nutzdaten abzuschließen:

* `min_feedback_data_size` - Dies ist die Mindestanzahl an Datensätzen in der Feedbackdatei, um eine Wiederholung des fortlaufenden Ausbildungssystems zu starten. 
* `auto_retrain` [never, always, conditionally] - Dieser Parameter gibt an, wann ein erneuter Trainingsprozess ausgelöst werden sollte. [conditionally] löst einen erneuten Trainingsprozess aus, wenn die Modellqualität unter den angegebenen Grenzwert fällt. 
* `auto_redeploy` [never, always, conditionally] - Dieser Paramater gibt an, wann ein erneut trainiertes Modell bereitgestellt werden sollte. [conditionally] löst die erneute Bereitstellung eines Modells aus, wenn die Qualität des neu trainierten Modells besser als die des aktuell bereitgestellten Modells ist. 


Anforderungsbeispiel:

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
           "connection": {
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

Ausgabebeispiel:
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

**Hinweis**: In diesem Beispiel werden die Standardwerte für die Parameter `auto_retrain` und `auto_redeploy` verwendet. Weitere Informationen zu diesen Parametern finden Sie in der [REST-API-Dokumentation](http://watson-ml-api.mybluemix.net/#!/Published32Models/put_v3_wml_instances_instance_id_published_models_published_model_id_learning_configuration) für den Parameter `learning_configuration`. 

## Führen Sie die fortlaufende Wiederholung des Ausbildungssystems aus. 

Verwenden Sie zum Starten der Wiederholung des Ausbildungssystems die unten dargestellte REST-API-Methode. Innerhalb der Wiederholung wird das veröffentlichte Modell evaluiert. Wenn die Evaluierungsgenauigkeit unter dem angegebenen Schwellenwertmodell liegt, wird ein erneutes Training ausgelöst. Beide Datensätze, der für das Training und der für das Feedback, werden für das erneute Training und die Evaluierung verwendet. 

Anforderungsbeispiel:

```
curl -X POST --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

Ausgabebeispiel:

```
Die Anforderung wurde erfüllt und im Ergebnis wurde eine neue Ressource erstellt.
```
{: codeblock}

Geben Sie die folgende Anforderung aus, um den Status der Wiederholung zu überprüfen: 

Anforderungsbeispiel:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

Ausgabebeispiel:

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
               },
               "version":"2.0"
            }
         }
      },
   ]
}
```
{: codeblock}

Sie können auch die Liste der Evaluierungsmetriken und Werte abrufen, indem Sie die folgende Anforderung ausgeben: 

Anforderungsbeispiel:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/evaluation_metrics
```
{: codeblock}

Ausgabebeispiel:

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
