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

# Streamingmodelle bereitstellen <span class='tag--beta'>Beta</span>

**Hinweis:** Diese Funktion ist aktuell nur als Betaversion vorhanden und steht nur für die Verwendung mit Spark MLlib zur Verfügung. Wenn Sie daran teilnehmen möchten, fügen Sie sich selbst zur Warteliste hinzu! Weitere
Informationen finden Sie unter [https://www.ibm.biz/mlwaitlist](https://www.ibm.biz/mlwaitlist).

**Szenarioname:** Stimmungsanalyse.

**Szenariobeschreibung:** Eine Marketing-Agentur möchten die
Stimmung zu einem bestimmten Thema erfassen. Die Agentur erwartet, dass wir ein Modell entwickeln, das
eine gemachte Aussage als positiv (POSITIVE) oder
negativ (NEGATIVE) einstuft. Ein Data-Scientist bereitet ein
Vorhersagemodell vor und teilt es mit Ihnen (dem Entwickler). Ihre Aufgabe ist es, das Modell bereitzustellen und eine
Vorhersageanalyse zu generieren, indem Sie Scoring-Anforderungen für
das implementierte Modell erstellen.

In diesem [Dokument](https://github.com/pmservice/tweet-sentiment-prediction) finden Sie weitere Informationen.

## Beispielmodell verwenden

1. Wechseln Sie zur Registerkarte Beispiele des IBM® Watson™ Machine Learning-Dashboards.
2. Suchen Sie im Abschnitt Beispielmodelle die Kachel für die Stimmungsvorhersage
und klicken Sie auf die Schaltfläche Modell hinzufügen (+).

Jetzt sehen Sie das Beispielmodell zur Stimmungsvorhersage in der
Liste mit verfügbaren Modellen auf der Registerkarte Modelle.


## Streamingbereitstellung mit IBM Message Hub erstellen

1.  Wechseln Sie zur Registerkarte 'Modelle' des IBM® Watson™ Machine Learning-Dashboards. 
2.  Wählen Sie im Menü AKTIONEN die Option zum Erstellen einer Bereitstellung. 
3.  Geben Sie im Formular zum Erstellen einer Bereitstellung den Namen, eine Beschreibung und den Datenstromtyp an. 
4.  Sie müssen die folgenden Eingaben bereitstellen:

    **Eingabeverbindung**: IBM Message Hub-Themen, die als Eingabe (Tweets) für
das Modell verwendet werden, und der Speicherort für die
Modellausgabe (Vorhersageergebnisse). 

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

    **Ausgabeverbindung**

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

    **Spark-Verbindung**: Berechtigungsnachweise für den Spark-Service finden Sie auf der Registerkarte für Serviceberechtigungsnachweise im Servicedashboard für Bluemix Spark.

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

5. Klicken Sie auf **Speichern**.

Das Vorhersageergebnis wird an das definierte MessageHub-Thema (Ausgabeverbindung) gesendet.

## Bereitstellungsdetails abrufen

Sie können den Status und Parameter im Zusammenhang mit den implementierten Modellen überprüfen.

1. Wechseln Sie zur Registerkarte 'Bereitstellungen' des IBM® Watson™ Machine Learning-Dashboards.


2. Klicken Sie im Menü **Aktionen** auf **Details anzeigen**.

## Eine Streamingbereitstellung löschen

Sie können die Bereitstellung mit einer Abfrage wie im folgenden Beispiel
löschen, wenn diese nicht mehr benötigt wird

1. Wechseln Sie zur Registerkarte 'Bereitstellungen' des IBM® Watson™ Machine Learning-Dashboards.


2. Wählen Sie im Menü AKTIONEN die Option zum Löschen aus.
