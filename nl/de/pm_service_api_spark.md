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

# Service-API


Der Machine Learning-Service
besteht aus einer Gruppe von
REST-APIs,
die über jede Programmiersprache aufgerufen werden können und die die
Integration von mit Data Science Experience entwickelten Analysen in
Ihre Anwendungen erlauben. Binden Sie Ihre Bluemix-Anwendungen an die Machine Learning-Serviceinstanz
und generieren Sie die Vorhersageanalyse, die Ihre Anwendungen benötigen, um Ihren Benutzern eine
höhere Wertschöpfung zu ermöglichen. Verwalten Sie Modelle im [Administrationsdashboard](pm_service_ui_spark.html) und
verwenden Sie das Dashboard, um Online-, Stapel- oder
Streamingbereitstellungen zu erstellen, die in Ihre Anwendungen
integriert sind. 

Entwickeln Sie Anwendungen für die Data Science Experience-Dateien (Spark- und Python-Modelle), die über die
leistungsfähigen [REST-APIs](https://watson-ml-api.mybluemix.net/) in einer Serviceinstanz bereitgestellt werden:

*  Metadaten für ein gegebenes Vorhersagemodell abrufen
*  Modelle bereitstellen und bereitgestellte Modelle verwalten
    *  Onlinebereitstellung (Scoring)
    *  Stapelbereitstellung (unterstützt Db2 Warehouse on Cloud)
    *  Streamingbereitstellung (mit Unterstützung für IBM
Message Hub)
*  Metadaten für eine gegebene Bereitstellung abrufen
*  Vorhersageanalysen generieren, indem
Sie
Scoring-Anforderungen für implementierte Vorhersagemodelle erstellen

In den folgenden Abschnitten finden Sie Beispiele für die Verwendung der REST-API:

*  [Onlinebereitstellung und Scoring](pm_service_api_spark_online.html)
*  [Stapelbereitstellung mit Db2 Warehouse on Cloud](pm_service_api_spark_batch.html)
*  [Streamingbereitstellung mit Message Hub](pm_service_api_spark_streaming.html)
