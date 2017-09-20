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

Das fortlaufende Ausbildungssystem von IBM® Watson™ Machine Learning bietet eine automatisierte Überwachung des Modellerfolgs, erneutes Training und erneute Bereitstellung zur Sicherung der Vorhersagequalität. 

**Szenarioname**: Beste Auswahl für ein Medikament zur Herzbehandlung.

**Szenariobeschreibung**: Ein Biomedizinisches Unternehmen, das Herzmedikamente herstellt, möchte ein Modell bereitstellen, das das jeweils beste Medikament für die Herzbehandlung auswählt. Wenn neue Nachweise zur Wirksamkeit des Medikaments auftauchen, sollte eine Modellaktualisierung in Erwägung gezogen werden. Ein Data-Scientist bereitet ein Vorhersagemodell vor und teilt es mit Ihnen (dem Entwickler). Ihre Aufgabe ist es, das Modell bereitzustellen, die Konfiguration für die Schulung zu definieren und eine Lernwiederholung durchzuführen, um das Modell zu evaluieren, erneut zu trainieren und erneut bereitzustellen. 

## Beispielmodell verwenden

1. Wechseln Sie zur Registerkarte Beispiele des IBM® Watson™ Machine Learning-Dashboards.

2. Suchen Sie im Abschnitt mit den Beispielmodellen das Beispiel mit der Kachel 'Heart Drug Selection'
   und klicken Sie auf die Schaltfläche zum Hinzufügen eines Modells (+).

Das Modell für die Auswahl des Herzmedikaments wird in der Liste der verfügbaren Modelle auf der Registerkarte 'Modelle' angezeigt. 


## Fortlaufendes Ausbildungssystem für das veröffentlichte Modell festlegen

1.  Wechseln Sie zur Registerkarte 'Modelle' des IBM® Watson™ Machine Learning-Dashboards. 

2.  Klicken Sie im Menü **Aktionen** auf **Details anzeigen**.

3.  Blättern Sie zu **Erneutes Training - Details** und drücken Sie **Bearbeiten**.

4.  Sie müssen die folgenden Eingaben bereitstellen. 

    **Feedback Verbindung**: Details zu Db2 Warehouse on Cloud, die als Eingabe (Feedbackdaten) für die Modellevaluation und das erneute Training verwendet werden.
    
    ```
    {
        "connection": {
            "username": "dash102204",
            "host": "awh-yp-small02.services.dal.bluemix.net",
            "password": "NweTlYwPY6cu",
            "db": "BLUDB"
        },
    "source": {
            "type": "dashdb",
            "tablename": "DRUG_FEEDBACK_DATA"
        }
    }
    ```
    {: codeblock}

    Verwenden Sie die folgenden Anweisungen, um die Tabelle `DRUG_FEEDBACK_DATA` in Db2 Warehouse on Cloud vorzubereiten.
    - Erstellen Sie eine Instanz von [Db2 Warehouse on Cloud Service](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/) (ein Eingabeplan wird angeboten). 
    - Erstellen Sie die Tabelle **DRUG_FEEDBACK_DATA** in **Db2 Warehouse on Cloud**.
      + Laden Sie die Datei [drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv) vom git-Repository herunter.
      + Klicken Sie auf **Konsole öffnen**, damit das Symbol **Db2 Warehouse on Cloud** als Beginn angezeigt wird. 
      + Wählen Sie die Option **Daten laden** und den Ladetyp **Desktop** aus. 
      + Wählen Sie für die zuvor heruntergeladene Datei **Ziehen und Ablegen** aus und klicken Sie auf **Weiter**.
      + Wählen Sie **Schema** aus, um Daten zu importieren und klicken Sie auf **Neue Tabelle**.
      + Schreiben Sie einen Namen für die **neue Tabelle** und klicken Sie anschließend auf **Weiter**, um den Datenimport zu beenden. 
      + Verwenden Sie `;` als **Feldtrennzeichen**.
      + Klicken Sie auf **Weiter**, um eine Tabelle mit den hochgeladenen Daten zu erstellen. 

    **Hinweis**: Sie können neue Feedbackdatensätze zur Feedbackdatenbank hinzufügen, indem Sie diesen [REST-API-Endpunkt](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback) verwenden.

    **Minimale Datengröße**: Die minimale Anzahl der Datensätze im Feedbackdatensatz zum Starten der Evaluierung des Modells (Teil der Wiederholung des Ausbildungssystems). 

    ```
    20
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

    **Schwellenwerte**: Der Grenzwert, der den erneuten Trainingsprozess auslöst (Bei einer Berechnung während der Evaluierung liegt der Metrikwert unter dem Grenzwert.)
    ```
    0.8
    ```

    **Erneut trainiertes Modell automatisch bereitstellen**: Erneut trainiertes Modell bereitstellen, wenn es eine bessere Qualität aufweist (Metrikwerte) als das aktuell bereitgestellte Modell.
5.  Klicken Sie auf die Option zum **Konfigurieren**.


## Führen Sie die fortlaufende Wiederholung des Ausbildungssystems aus. 

Innerhalb der Wiederholung wird das veröffentlichte Modell evaluiert. Wenn die Evaluierungsgenauigkeit unter dem angegebenen Schwellenwertmodell liegt, wird ein erneutes Training ausgelöst. Beide Datensätze, der für das Training und der für das Feedback, werden für das erneute Training und die Evaluierung verwendet. 

1. Zum Starten einer neuen Wiederholung klicken Sie im Formular **Details** auf der Registerkarte **Überwachen** auf **Evaluieren**.

3. Um das Ergebnis der Wiederholung zu überprüfen, wechseln Sie entweder in die Tabelle mit den Evaluierungsergebnissen oder in die Diagrammansicht. Dort finden Sie Informationen zur Modellqualität, die auf Grundlage von Feedbackdaten (Überwachung) und der Qualität des erneut trainierten Modells (neu erstellte und evaluierte Modellversion) berechnet wurden. 

4. >Zum Anzeigen einer Liste automatisch trainierter Modelle und deren Qualität wechseln Sie zum Versionsprotokoll, das sich unten auf der Registerkarte mit der Übersicht befindet (Detailanzeige zum Modell -> Übersicht).
