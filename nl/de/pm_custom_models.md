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

# Entwicklung und Persistenz des angepassten Modells

## Mit angepassten Modellen arbeiten

### Szenarioname: Produktlinienvorhersage.

### Szenariobeschreibung:

Unser Kunde führt
eine der bekanntesten Handelsketten in Europa. Er möchte, dass wir herausfinden, an welcher Produktlinie die Kunden jeweils interessiert sind, z. B. persönliche Accessoires, Campingausrüstung oder Outdoorschutz.
Ein Data-Scientist entwickelt ein Vorhersagemodell und
teilt es mit Ihnen (dem Entwickler). Ihre Aufgabe ist es, das Modell bereitzustellen und eine
Vorhersageanalyse zu generieren, indem Sie Scoring-Anforderungen für
das implementierte Modell erstellen.

### Entwicklung und Persistenz des angepassten Modells

Verwenden Sie Data Science
Experience, um angepasste Modelle zu erstellen. Melden Sie sich nach der Registrierung an und führen Sie die folgenden Schritte aus.

1. Eine Organisation und einen Bereich erstellen. Wenn Sie sich das erste Mal anmelden, werden Sie aufgefordert, diese anzugeben, also klicken Sie auf **Weiter** und akzeptieren die Standardwerte. 

2. Wechseln Sie, nachdem die Organisation erstellt wurde, zu **Projekte** und klicken Sie auf **Neues Projekt**.

3. Geben Sie einen Namen und eine Beschreibung für Ihr
Projekt an und klicken Sie auf **Erstellen**. Der
angegebene Projektname wird auch als Name Ihres Zielcontainers
verwendet.

4. Nachdem das Projekt erstellt wurde, können Sie entweder: 
   *  **Notizbücher hinzufügen** und mit der Entwicklung Ihrer eigenen Modelle
beginnen oder eines der folgenden Beispielnotizbücher hochladen:

    *  [Entwickeln von Spark MLlib-Modellen mit Python](https://apsportal.ibm.com/analytics/notebooks/89492fd6-a641-4819-9176-3d9381561df9/view?access_token=d80bef1a172d1d83d3721b101886337158457281774186f181a2e6a5b57f5ec7)

    *  [Entwickeln von Spark MLlib-Modellen mit Scala](https://apsportal.ibm.com/analytics/notebooks/c8652d2c-bfc9-4354-8168-f1c9f7f8dfc2/view?access_token=02a83fea8450a452c8de76af98dae078459d0f56810ddef4f4c62d5bc4fc72cf)

    *  [Entwickeln von scikit-learn-Modellen mit Python](https://apsportal.ibm.com/analytics/notebooks/5215a61a-16d7-4fa2-b060-e3e243ceebe3/view?access_token=70f48c95c5571a614ce97484d3f168b1d9b6aeebce015187d3d77ce6038f025e)

   * **Modelle hinzufügen** und mit der Entwicklung Ihrer eigenen Modelle mithilfe des Modellassistenten beginnen. 



### Bereitstellung und Scoring des angepassten Modells

Anweisungen für Bereitstellungs- und Scoring-Modelle finden Sie
in den folgenden Abschnitten oder im Abschnitt zum Scoring in
den oben verlinkten Notizbüchern.

*  [Onlinemodelle bereitstellen](pm_service_api_spark_online.html)

*  [Stapelmodelle bereitstellen](pm_service_api_spark_batch.html)

*  [Streamingmodelle bereitstellen](pm_service_api_spark_streaming.html)
