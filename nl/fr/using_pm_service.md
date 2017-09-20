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

# Utilisation du service

Les méthodes de modélisation disponibles dans la palette de modélisation de SPSS Modeler
vous permettent de puiser de nouvelles informations dans vos données et de développer des
modèles prédictifs. Chaque méthode possède ses propres avantages et
est donc plus adaptée à certains types de problème spécifiques.
{: .shortdesc}

Pour plus d'informations
sur SPSS Modeler et les algorithmes de modélisation qu'il utilise, reportez-vous à la documentation du site
[IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7).

Une fois que vous avez implémenté les exigences en matière d'entrée et de sortie de votre application Bluemix et de conception de la branche d'évaluation SPSS Modeler, votre analyste de
données peut modifier n'importe quel aspect interne de cette branche. Il peut même modifier le ou les algorithmes de modélisation utilisés dans une opération d'actualisation afin que vous puissiez ensuite affiner vos analyses prédictives sans devoir réécrire vos applications.


## Etapes de liaison du service avec l'application Bluemix
Suivez les étapes suivantes pour créer votre application Bluemix et la lier au service Machine Learning.

1. Téléchargez l'exemple de code d'application Node.js du [référentiel github](https://github.com/pmservice/customer-satisfaction-prediction).

2. Utilisez la commande cf create-service pour créer une instance de service :

   ```
   cf create-service pm-20 Free {local naming}
   ```
   {: codeblock}

   Par exemple :

   ```
   cf create-service pm-20 Free my_pm_free
   ```
   {: codeblock}

   Cette commande dans votre espace Bluemix crée une instance de service Machine Learning nommée
my_pm_free avec le plan gratuit (Free).

3. Utilisez la commande `cf create-service-key` pour créer des données d'identification pour le service :

   ```
   cf create-service-key "{nom_instance_service}" {nom_clé_vcap}
   ```
   {: codeblock}

   Par exemple :

   ```
   cf create-service-key "IBM Watson Machine Learning - my instance" Credentials-1
   ```
   {: codeblock}

   Cette commande crée les données d'identification du service Machine Learning.

4. Utilisez la commande cf bind-service pour lier l'instance de service my_pm_free à votre application.

   ```
   cf bind-service AppName my_pm_service
   ```
   {: codeblock}

   Par exemple :

   ```
   cf bind-service my_app1 my_pm_free
   ```
   {: codeblock}

   Cette commande lie l'instance de service Machine Learning nommée `my_pm_free` à l'application Bluemix my_app1.

5. Données d'identification Machine Learning :

   Après avoir lié l'instance de service Machine Learning à votre application Bluemix, les données d'identification Machine Learning sont ajoutées à la variable d'environnement `VCAP_SERVICES` :

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

   La variable d'environnement `VCAP_SERVICES` contient les informations suivantes :

   <dl>

   <dt>plan</dt>
   <dd>Plan Machine Learning utilisé pour la mise à disposition du service.</dd>

   <dt>url</dt>
   <dd>Adresse de l'instance de service Machine Learning.</dd>

   <dt>access_key</dt>
   <dd>Paramètre de requête accessKey via lequel sont transmises toutes les requêtes à cette instance de service.</dd>

   </dl>

Par exemple :             

```
Get https://ibm-watson-ml.mybluemix.net/pm/v1/model/sales_model2?accesskey=XXXXXXXXXXXXX
```
{: codeblock}

   Exemple de code Node.js illustrant comment obtenir la valeur de accessKey depuis la variable d'environnement `VCAP_SERVICES` :

```
   if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var credentials = env['pm-20'][0].credentials;
        var accessKey = credentials.access_key;
    }
```
{: codeblock}
