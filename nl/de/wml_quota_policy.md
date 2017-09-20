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

# Kontingentrichtlinie

Die IBM Watson Machine Learning Engine erzwingt bestimmte Kontingente pro Instanz, um eine entsprechende Ressourcenzuordnung und -nutzung zu gewährleisten. Diese Richtlinien variieren je nach Kontoprofil, Protokollserviceverwendung und Verfügbarkeit der Ressourcen. Die Kontingentrichtlinie beschreibt Grenzwerte, die nicht durch die Preisstruktur definiert sind und **ohne vorherige Ankündigung geändert werden können**. 

Die folgenden Servicekontingentgrenzwerte sind momentan aktiv. 

## Ressourcennutzung

Ressourcen sind auf die folgenden Maximalwerte begrenzt: 

-  **Maximal veröffentlichte Modelle**: 200 (kostenfreier Plan) 1000 (Standardplan & professioneller Plan)
-  **Maximale Spark-ML-Modellgröße**: 200 MB
-  **Maximal implementierte Modelle**: 1000 (Standardplan & professioneller Plan)

**Anmerkung**: Um die Grenzwerte des kostenfreien Plans zu verstehen, lesen Sie die Beschreibung zum Thema [kostenfreier Plan](https://console.bluemix.net/catalog/services/machine-learning) in [Bluemix-Katalog](https://console.bluemix.net/catalog/).

## Serviceanforderungsgrenzen

Die Anzahl der Anforderungen, die Sie pro Minute an eine bestimmte API senden können, ist begrenzt. Wenn Ihre Anwendung einen höheren Grenzwert erfordert, müssen Sie sich mit [IBM Bluemix Support](https://support.ng.bluemix.net/) in Verbindung setzen, um Ihr Kontingent zu erhöhen. 

## Bereitstellungsanforderungen

Die folgenden Grenzwerte gelten für die Anforderungen an die Bereitstellungs-API:

-  **Zeitraum**: 60 Sekunden
-  **Standardgrenzwert**: 10

## Online-Prognoseanforderungen

Die folgenden Grenzwerte gelten für Anforderungen für eine [Online-Prognose](pm_service_api_spark_building.html):

-  **Zeitraum**: 60 Sekunden
-  **Standardgrenzwert**: 500

## Ressourcenmanagementanforderungen

Die folgenden Grenzwerte gelten für die kombinierten Gesamtanforderungen in dieser Liste: 

[Token](https://watson-ml-api.mybluemix.net/#/Token): Anforderungen: post, get, delete, put, patch

[Bereitstellungen](https://watson-ml-api.mybluemix.net/#/Deployments): Anforderungen post, get, delete, put, patch 

-  **Zeitraum**: 60 Sekunden
-  **Standardgrenzwert**: 100
