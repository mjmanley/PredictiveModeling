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

# Utilizzo del servizio

I metodi di modellazione disponibili nella tavolozza dei modelli SPSS Modeler ti consentono di ricavare nuove
informazioni dai tuoi dati e di sviluppare modelli predittivi. Ogni metodo ha determinati punti di forza e si presta meglio per particolari tipi di problemi.
{: .shortdesc}

Per i dettagli su SPSS Modeler e sugli algoritmi di modellazione che fornisce, consulta [IBM
Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7).

Dopo che sono stati implementati i requisiti di input e di output della progettazione della tua applicazione Bluemix e
del ramo di calcolo del punteggio SPSS Modeler, il tuo analista dei dati può modificare qualsiasi aspetto interno del ramo di calcolo del
punteggio. L'analista dei dati può anche modificare uno o più algoritmi di modello utilizzati in un'operazione di aggiornamento, assicurandoti di poter ottimizzare la tua analisi predittiva senza dover riscrivere le tue applicazioni.


## Procedura per eseguire il bind del servizio all'applicazione Bluemix
Completa la seguente procedura per creare la tua applicazione Bluemix ed eseguirne il bind al servizio Machine Learning.

1. Scarica il codice dell'applicazione di esempio Node.js dal [repository github](https://github.com/pmservice/customer-satisfaction-prediction).

2. Utilizza il comando cf create-service per creare un'istanza del
   servizio:

   ```
   cf create-service pm-20 Free {local naming}
   ```
   {: codeblock}

   Ad esempio:

   ```
   cf create-service pm-20 Free my_pm_free
   ```
   {: codeblock}

   Questo comando crea un'istanza del servizio Machine Learning
   con il piano Gratuito denominato my_pm_free nel tuo spazio Bluemix.

3. Utilizza il comando `cf create-service-key` per creare le credenziali del servizio:

   ```
   cf create-service-key "{service instance name}" {vcap key name}
   ```
   {: codeblock}

   Ad esempio:

   ```
   cf create-service-key "IBM Watson Machine Learning - my instance" Credentials-1
   ```
   {: codeblock}

   Questo comando crea le credenziali del servizio Machine Learning.

4. Utilizza il comando cf bind-service per eseguire il bind dell'istanza del servizio
   my_pm_free alla tua applicazione.

   ```
   cf bind-service AppName my_pm_service
   ```
   {: codeblock}

   Ad esempio:

   ```
   cf bind-service my_app1 my_pm_free
   ```
   {: codeblock}

   Questo comando esegue il bind dell'istanza del servizio Machine Learning
   `my_pm_free` all'applicazione Bluemix my_app1.

5. Credenziali di Machine Learning:

   Dopo che hai eseguito il bind dell'istanza del servizio Machine Learning alla tua
   applicazione Bluemix, le credenziali di Machine Learning vengono
   aggiunte alla variabile di ambiente `VCAP_SERVICES`:

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

   La variabile di ambiente `VCAP_SERVICES` include le seguenti informazioni:

   <dl>

   <dt>piano</dt>
   <dd>Il piano Machine Learning utilizzato nel provisioning del servizio.</dd>

   <dt>url</dt>
   <dd>L'indirizzo dell'istanza del servizio Machine Learning.</dd>

   <dt>chiave_accesso</dt>
   <dd>Il parametro di query accessKey da passare in tutte le richieste
            a questa istanza del servizio.</dd>

   </dl>

Ad esempio:             

```
Get https://ibm-watson-ml.mybluemix.net/pm/v1/model/sales_model2?accesskey=XXXXXXXXXXXXX
```
{: codeblock}

   Codice Node.js di esempio che mostra come ottenere l'accessKey dalla
   variabile di ambiente `VCAP_SERVICES`:

```
   if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var credentials = env['pm-20'][0].credentials;
        var accessKey = credentials.access_key;
    }
```
{: codeblock}
