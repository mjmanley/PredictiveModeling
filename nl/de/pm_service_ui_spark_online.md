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

# Onlinemodelle bereitstellen


**Szenarioname:** Produktlinienvorhersage.

**Szenariobeschreibung:** Eine Firma für Outdoorausrüstung möchte
ein Modell erstellen, das das Kundeninteresse an ihren Produktlinien
vorhersagt. Ein Data-Scientist entwickelt ein Vorhersagemodell und
teilt es mit Ihnen (dem Entwickler). Ihre Aufgabe ist es, das Modell bereitzustellen und eine Vorhersage zu generieren, indem Sie
Scoring-Anforderungen für das implementierte Modell erstellen.

## Beispielmodell verwenden

1. Wechseln Sie zur Registerkarte Beispiele des IBM® Watson™ Machine Learning-Dashboards.

2. Suchen Sie im Abschnitt Beispielmodelle die Kachel für die Produktlinienvorhersage
und klicken Sie auf die Schaltfläche Modell hinzufügen (+).

Jetzt sehen Sie das Beispielmodell
zur Produktlinienvorhersage in der Liste mit verfügbaren Modellen auf der Registerkarte
Modelle.


## Onlinebereitstellung erstellen

1. Wechseln Sie zur Registerkarte 'Modelle' des IBM® Watson™ Machine Learning-Dashboards. 

2. Wählen Sie im Menü AKTIONEN die Option zum Erstellen einer Bereitstellung aus. 

3. Geben Sie im Formular zum Erstellen einer Bereitstellung den Namen, eine Beschreibung und den Onlinetyp an. 

4. Klicken Sie auf die Schaltfläche zum Speichern. 

Jetzt wird die Onlinebereitstellung in der Liste der verfügbaren Bereitstellungen auf der Registerkarte mit den Bereitstellungen angezeigt. 


## Bereitstellungsdetails abrufen

Sie können den Status, die Scoring-Endpunktadresse (`Scoring-Endpunkt`) und die Parameter des
Bereitstellungsmodells prüfen. 

1. Wechseln Sie zur Registerkarte 'Bereitstellungen' des IBM® Watson™ Machine Learning-Dashboards. 

2. Wählen Sie im Menü AKTIONEN die Option zum Anzeigen der Details aus. 

Beachten Sie, dass der Wert für `Scoring-Endpunkt` erforderlich ist, um im nächsten Schritt eine Scoring-Anforderung zu erstellen. 


## Scoring-Anforderungen stellen

Da Ihr Scoring-Endpunkt erstellt wurde (`Scoring-Endpunkt`), können
Sie jetzt Vorhersagen mithilfe von Scoring-Anforderungen generieren. In diesem Szenario werden
Kundendatensätze an das Vorhersagemodell übergeben und es wird eine
Vorhersage für ein Sportprodukt zurückgegeben.

Beispieldatensatzheader:

```
GENDER,AGE,MARITAL_STATUS,PROFESSION
```
{: codeblock}

Beispieldatensatz:

```
M,27,Single,Professional
F,56,Unspecified,Hospitality
M,45,Married,Retired
```
{: codeblock}

Anforderungsbeispiel:

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: Bearer  $token' -d '{"fields": ["GENDER","AGE","MARITAL_STATUS","PROFESSION"],"values": [["M",23,"Single","Student"],["M",55,"Single","Executive"]]}' https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/deployments/{deployment_id}/online
```
{: codeblock}

Ausgabebeispiel:

```
{
   "fields": ["GENDER",
      "AGE",
      "MARITAL_STATUS",
      "PROFESSION",
      "PROFESSION_IX",
      "GENDER_IX",
      "MARITAL_STATUS_IX",
      "features",
      "rawPrediction",
      "probability",
      "prediction",
      "predictedLabel"
   ],
   "records":[
      [
         "M",
         23,
         "Single",
         "Student",
         6.0,
         0.0,
         1.0,
         [
            0.0,
            23.0,
            1.0,
            6.0
         ],
         [
            5.600716147152702,
            6.482458372136143,
            6.048004170730676,
            0.20929155492307386,
            1.6595297550574055
         ],
         [
            0.2800358073576351,
            0.32412291860680714,
            0.3024002085365338,
            0.010464577746153694,
            0.08297648775287028
         ],
         1.0,
         "Personal Accessories"
      ],
      [
         "M",
         55,
         "Single",
         "Executive",
         3.0,
         0.0,
         1.0,
         [
            0.0,
            55.0,
            1.0,
            3.0
         ],
         [
            6.227653744886563,
            4.325198862164969,
            8.031953760146816,
            1.2319759269281225,
            0.1832177058735289
         ],
         [
            0.3113826872443282,
            0.2162599431082485,
            0.40159768800734086,
            0.06159879634640614,
            0.009160885293676447
         ],
         2.0,
         "Mountaineering Equipment"
      ]
   ]
}
```
{: codeblock}

Wir können beispielsweise erkennen, dass ein 55 Jahre alter Angestellter sich
für Bergsteigerausrüstung interessiert, während ein 23 Jahre alter Student sich für
Persönliches Zubehör interessiert.
