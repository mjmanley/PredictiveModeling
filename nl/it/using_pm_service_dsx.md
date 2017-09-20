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

Prendi nota delle seguenti informazioni importanti riguardo il servizio Machine
Learning.

## Procedura per eseguire il bind del servizio all'applicazione Bluemix

Puoi scaricare il [codice di esempio](https://github.com/pmservice/product-line-prediction/blob/master/README.md) Node.js per provare il servizio Machine
Learning. Completa la seguente procedura per creare la tua applicazione Bluemix ed eseguire il bind del servizio Machine Learning. Questi esempi utilizzano Node.js perché è un runtime di uso comune. È possibile utilizzarne degli altri come iOS, Ruby, Perl o Java.

Nota che puoi anche effettuare i passi 1-3 utilizzando l'interfaccia grafica Bluemix al posto dello strumento Cloud Foundry (cf).

1. Utilizza il comando `cf create-service` per creare un'istanza del servizio:

   ```
   cf create-service pm-20 Free {local naming}
   ```
   {: codeblock}

   Ad esempio:

   ```
   cf create-service pm-20 Free my_wml_free
   ```
   {: codeblock}

   Questo comando crea un'istanza del servizio Machine Learning
   con il piano Gratuito denominato `my_wml_free` nel tuo spazio Bluemix.

2. Utilizza il comando `cf create-service-key` per creare le credenziali del servizio:

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

3. Utilizza il comando cf bind-service per eseguire il bind dell'istanza del servizio
   `my_wml_free` alla tua applicazione.

   ```
   cf bind-service {AppName} my_wml_free
   ```
   {: codeblock}

   Ad esempio:

   ```
   cf bind-service my_app1 my_wml_free
   ```
   {: codeblock}

   Questo comando esegue il bind dell'istanza del servizio Machine Learning
   `my_wml_free` all'applicazione Bluemix `my_app1`.



## Credenziali di Machine Learning

Dopo che hai eseguito il bind dell'istanza del servizio Machine Learning alla tua
   applicazione Bluemix, le credenziali di Machine Learning vengono
   aggiunte alla variabile di ambiente `VCAP_SERVICES`:

```
    {
     "pm-20-dev": [
       {
         "credentials": {
           "url":
           "https://ibm-watson-ml.mybluemix.net",
           "access_key": "**********",
           "username": "**********",
           "password": "**********",
           "instance_id": "**********"
         },
           "label": "pm-20-dev",
           "plan": "Free",
           "name": "IBM Watson Machine Learning”
       }
     ]
    }
```
{: codeblock}

   La variabile di ambiente `VCAP_SERVICES` include le seguenti informazioni:

   * `plan` - il piano Machine Learning utilizzato nel provisioning del servizio.
   * `url` - l'indirizzo dell'istanza del servizio Machine Learning.
   * `access_key` - solo per i flussi SPSS Modeler.
   * `instance_id` - identificativo univoco dell'istanza Machine Learning.
   * `username`, `password` - autorizzazione di base necessaria per generare un token di accesso per passare tutte le richieste a questa istanza del servizio. Ad esempio, puoi generare un token di accesso utilizzando un curl come questo:

Esempio di
richiesta:

```
       curl --basic --user {username}:{password} https://ibm-watson-ml.mybluemix.net/v3/identity/token

       Esempio di
output:

       {"token":"**********"}
```
{: codeblock}

   Il seguente codice Node.js è un esempio di come ottenere
   l'username e password dalla variabile di ambiente
   `VCAP_SERVICES`:

```
   if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var credentials = env['pm-20'][0].credentials;
        var username = credentials.username;
        var password = credentials.password;
        var instance_id = credentials.instance_id;
    }
```
{: codeblock}
