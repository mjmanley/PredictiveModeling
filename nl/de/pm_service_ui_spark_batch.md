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

# Stapelmodelle bereitstellen <span class='tag--beta'>Beta</span>

**Hinweis:** Diese Funktion ist aktuell nur als Betaversion vorhanden und steht nur für die Verwendung mit Spark MLlib zur Verfügung. Wenn Sie daran teilnehmen möchten, fügen Sie sich selbst zur Warteliste hinzu! Weitere
Informationen finden Sie unter [https://www.ibm.biz/mlwaitlist](https://www.ibm.biz/mlwaitlist).

**Szenarioname:** Kundenzufriedenheitsvorhersage.

**Szenariobeschreibung:** Ein Telekommunikationsunternehmen möchte wissen, bei welchen Kunden die Gefahr besteht, dass sie zu
einem anderen Anbieter wechseln. Das dargestellte Modell macht eine Vorhersage zur Abwanderung von Kunden. Ein Data-Scientist entwickelt ein Vorhersagemodell und teilt es mit Ihnen (dem Entwickler). Ihre Aufgabe ist es, das Modell bereitzustellen und eine
Vorhersageanalyse zu generieren, indem Sie Scoring-Anforderungen für
das implementierte Modell erstellen.

## Beispielmodell verwenden

1.  Wechseln Sie zur Registerkarte Beispiele des IBM® Watson™ Machine Learning-Dashboards.

2.  Suchen Sie im Abschnitt Beispielmodelle die Kachel für die Kundenzufriedenheitsvorhersage
und klicken Sie auf die Schaltfläche Modell hinzufügen (+).

Jetzt sehen Sie das Beispielmodell Kundenzufriedenheitsvorhersage in
der Liste mit verfügbaren Modellen auf der Registerkarte Modelle.

## Stapelbereitstellung mit Object Storage erstellen

1.  Wechseln Sie zur Registerkarte 'Modelle' des IBM® Watson™ Machine Learning-Dashboards. 

2.  Klicken Sie im Menü **Aktionen** auf **Bereitstellung erstellen**.

3.  Geben Sie im Formular 'Bereitstellung erstellen' den Namen, die Beschreibung und einen Batch-Typ an. 

4.  Sie müssen die folgenden Eingaben bereitstellen:

    **Eingabeverbindung**: Object Storage-Details, die als Eingabe (zu bewertende Kundendaten) für das
Modell verwendet werden, und der Speicherort für die Modellausgabe (in diesem Fall
die Datei results.csv, die automatisch erstellt wird). 

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

    ** Ausgabeverbindung **

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

5.  Klicken Sie auf **Speichern**.

Das Vorhersageergebnis wird in einer '.csv'-Datei in
IBM Object Storage gespeichert. Im Folgenden finden Sie eine Beispielzeile.

Eingabedateivorschau:

```
customerID,gender,SeniorCitizen,Partner,Dependents,tenure,PhoneService,MultipleLines,InternetService,OnlineSecurity,OnlineBackup,DeviceProtection,TechSupport,StreamingTV,StreamingMovies,Contract,PaperlessBilling,PaymentMethod,MonthlyCharges,TotalCharges,Churn
7590-VHVEG,Female,0,Yes,No,1,No,No phone service,DSL,No,Yes,No,No,No,No,Month-to-month,Yes,Electronic check,29.85,29.85,No
5575-GNVDE,Male,0,No,No,34,Yes,No,DSL,Yes,No,Yes,No,No,No,One year,No,Mailed check,56.95,1889.5,No
3668-QPYBK,Male,0,No,No,2,Yes,No,DSL,Yes,Yes,No,No,No,No,Month-to-month,Yes,Mailed check,53.85,108.15,Yes
```
{: codeblock}

Ausgabedateivorschau:

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


## Bereitstellungsdetails abrufen

Sie können den Status und Parameter im Zusammenhang mit den implementierten Modellen überprüfen.

1. Wechseln Sie zur Registerkarte 'Bereitstellungen' des IBM® Watson™ Machine Learning-Dashboards.


2. Wählen Sie im Menü AKTIONEN die Option zum Anzeigen der Details aus.


## Eine Stapelbereitstellung löschen

Sie können die Bereitstellung mit einer Abfrage wie im folgenden Beispiel
löschen, wenn diese nicht mehr benötigt wird

1. Wechseln Sie zur Registerkarte 'Bereitstellungen' des IBM® Watson™ Machine Learning-Dashboards.


2. Wählen Sie im Menü AKTIONEN die Option zum Löschen aus.
