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

Tenez compte des informations importantes suivantes concernant le service Machine Learning.

## Etapes de liaison du service avec l'application Bluemix

Vous pouvez télécharger l'[exemple de code](https://github.com/pmservice/product-line-prediction/blob/master/README.md) Node.js pour essayer le service Machine Learning. Pour créer votre application Bluemix et lier le service Machine Learning, procédez comme suit. Ces
exemples utilisent Node.js car il s'agit d'un environnement d'exécution populaire. Vous pouvez en utiliser d'autres tels que iOS, Ruby, Perl ou Java.

Notez que vous pouvez également réaliser les étapes 1 à 3 via l'interface graphique de Bluemix au lieu de l'outil Cloud Foundry
(cf).

1. Créez une instance de service à l'aide de la commande `cf create-service`.

   ```
   cf create-service pm-20 Free {désignation locale}
   ```
   {: codeblock}

   Par exemple :

   ```
   cf create-service pm-20 Free my_wml_free
   ```
   {: codeblock}

   Cette commande crée dans votre espace Bluemix une instance de service Machine Learning nommée `my_wml_free` avec le plan gratuit (Free).

2. Utilisez la commande `cf create-service-key` pour créer des données d'identification pour le service :

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

3. Utilisez la commande cf bind-service pour lier l'instance de service `my_wml_free` à votre application.

   ```
   cf bind-service {nom_application} my_wml_free
   ```
   {: codeblock}

   Par exemple :

   ```
   cf bind-service my_app1 my_wml_free
   ```
   {: codeblock}

   Cette commande lie l'instance de service Machine Learning `my_wml_free` à l'application Bluemix `my_app1`.



## Données d'identification du service Machine Learning

Après avoir lié l'instance de service Machine Learning à votre application Bluemix, les données d'identification de Machine Learning sont ajoutées à la variable d'environnement
`VCAP_SERVICES` :

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

   La variable d'environnement `VCAP_SERVICES` contient les informations suivantes :

   * `plan` - plan de Machine Learning utilisé pour la mise à disposition du service.
   * `url` - adresse de l'instance de service Machine Learning.
   * `access_key` - pour les flux SPSS Modeler uniquement.
   * `instance_id` - identificateur unique de l'instance Machine Learning.
   * `username`, `password` - autorisation de base requise pour générer un jeton d'accès à transférer dans toutes les requêtes à cette instance de
service. Vous pourriez, par exemple, générer un jeton d'accès avec une commande curl similaire à ceci :

Exemple de requête :

```
       curl --basic --user {username}:{password} https://ibm-watson-ml.mybluemix.net/v3/identity/token

       Exemple de sortie :

       {"token":"**********"}
```
{: codeblock}

   L'exemple de code Node.js suivant montre comment obtenir le nom d'utilisateur et le mot de passe de la variable d'environnement `VCAP_SERVICES` :

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
