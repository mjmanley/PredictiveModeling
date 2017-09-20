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

# Service verwenden

Die in der SPSS Modeler-Modellierungspalette verfügbaren
Modellierungsmethoden
ermöglichen Ihnen die Ableitung neuer Informationen aus Ihren Daten
und die Entwicklung von Vorhersagemodellen. Jede Methode weist bestimmte Stärken auf und eignet sich für spezielle Problemtypen.
{: .shortdesc}

Details zum SPSS Modeler und den von ihm bereitgestellten Modellierungsalgorithmen finden Sie im [IBM
Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7).

Nachdem die Ein- und Ausgabeanforderungen Ihrer Bluemix-Anwendung
und das Design der Scoring-Verzweigung für SPSS Modeler
implementiert wurden, kann der Datenanalyst jeden internen Aspekt der
Scoring-Verzweigung ändern. Der Datenanalyst kann sogar die Modellalgorithmen ändern, die in einer Aktualisierungsoperation verwendet werden und so sicherstellen, dass die Vorhersageanalyse optimiert werden kann, ohne dass die Anwendungen neu programmiert werden müssen.


## Schritte zum Binden des Service an eine Bluemix-Anwendung
Führen Sie die folgenden Schritte aus, um Ihre Bluemix-Anwendung
   zu erstellen und an den Machine Learning-Service zu binden. 

1. Laden Sie den Beispielanwendungscode für Node.js aus dem [github-Repository](https://github.com/pmservice/customer-satisfaction-prediction) herunter.

2. Verwenden Sie den Befehl cf create-service, um eine Serviceinstanz zu erstellen:

   ```
   cf create-service pm-20 Free {local naming}
   ```
   {: codeblock}

   Beispiel:

   ```
   cf create-service pm-20 Free my_pm_free
   ```
   {: codeblock}

   Dieser Befehl erstellt eine Machine Learning-Serviceinstanz mit einem kostenfreien Plan (Free),
dem in Ihrem Bluemix-Bereich der Name my_pm_free zugeordnet ist.

3. Verwenden Sie den Befehl `cf
create-service-key`, um Serviceberechtigungsnachweise zu
erstellen:

   ```
   cf create-service-key "{service instance name}" {vcap key name}
   ```
   {: codeblock}

   Beispiel:

   ```
   cf create-service-key "IBM Watson Machine Learning - my instance" Credentials-1
   ```
   {: codeblock}

   Dieser Befehl erstellt Machine Learning-Serviceberechtigungsnachweise.

4. Verwenden Sie den Befehl cf bind-service, um die Serviceinstanz my_pm_free an Ihre Anwendung
zu binden.

   ```
   cf bind-service AppName my_pm_service
   ```
   {: codeblock}

   Beispiel:

   ```
   cf bind-service my_app1 my_pm_free
   ```
   {: codeblock}

   Dieser Befehl bindet die Machine Learning-Serviceinstanz `my_pm_free`
an die Bluemix-Anwendung my_app1.

5. Machine Learning-Berechtigungsnachweise:

   Nachdem Sie die Machine Learning-Serviceinstanz an Ihre Bluemix-Anwendung gebunden haben, werden die Machine Learning-Berechtigungsnachweise zur Umgebungsvariablen `VCAP_SERVICES` hinzugefügt:

```
    {   
        "pm-20": {
            "name": "pm20-1",
            "label": "pm-20",
            "plan": "Free",
            "credentials": {
                "url": "https://ibm-watson-ml.mybluemix.net",
                "access_key": "XXXXXXXXXXXXX"
            }
        }       
    }
```
{: codeblock}

   Die Umgebungsvariable `VCAP_SERVICES` umfasst die folgenden Informationen:

   <dl>

   <dt>plan</dt>
   <dd>Der Machine Learning-Plan, der für die Servicebereitstellung verwendet wird.</dd>

   <dt>url</dt>
   <dd>Die Adresse der Machine Learning-Serviceinstanz.</dd>

   <dt>access_key</dt>
   <dd>Der Abfrageparameter accessKey, der in allen Anforderungen an diese Serviceinstanz übergeben
werden muss.</dd>

   </dl>

Beispiel:             

```
Get https://ibm-watson-ml.mybluemix.net/pm/v1/model/sales_model2?accesskey=XXXXXXXXXXXXX
```
{: codeblock}

   Node.js-Beispielcode, in dem dargestellt ist, wie der Zugriffsschlüssel (accessKey)
aus der Umgebungsvariablen `VCAP_SERVICES` abgerufen werden kann:

```
   if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var credentials = env['pm-20'][0].credentials;
        var accessKey = credentials.access_key;
    }
```
{: codeblock}
