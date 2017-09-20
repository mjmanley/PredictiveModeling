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

# Déploiement de modèles de traitement par lots <span class='tag--beta'>Beta</span>

**Remarque **: cette fonctionnalité est actuellement en version bêta et n'est disponible que pour son utilisation avec Spark MLlib. Si vous désirez participer, inscrivez-vous sur la liste d'attente. Pour plus d'informations,  voir : [https://www.ibm.biz/mlwaitlist](https://www.ibm.biz/mlwaitlist).

**Nom du scénario **: Pronostic de satisfaction des clients.

**Description du scénario **: Une entreprise de télécommunications désire savoir quels clients risquent de les abandonner. Le modèle présenté pronostique une attrition de la clientèle. Un spécialiste des données développe un modèle prédictif et le partage avec vous (le développeur). Votre tâche consiste à déployer le modèle et à générer des analyses prédictives en effectuant des requêtes de score à partir du modèle déployé.

## Utilisation de l'exemple de modèle

1.  Accédez à l'onglet Exemples du tableau de bord IBM® Watson™ Machine Learning.

2.  Dans la section Exemples de modèles, recherchez la vignette Pronostic de satisfaction des clients et cliquez sur le bouton Ajouter le modèle (+).

Vous pouvez observer à présent l'exemple de modèle Pronostic de satisfaction des clients dans la liste des modèles disponibles sous l'onglet Modèles.

## Création d'un déploiement par lots à l'aide d'Object Storage

1.  Accédez à l'onglet Modèles du tableau de bord d'IBM® Watson™ Machine Learning.

2.  Dans le menu **Actions**, cliquez sur **Créer un déploiement**.

3.  Dans le formulaire Créer un déploiement, fournissez un nom, une description et un type de traitement par lots.

4.  Vous devez fournir les informations suivantes :

    **Input Connection** : détails de Object Storage qui seront utilisés comme entrées (données clients auxquelles attribuer un score) pour le modèle et lieu de stockage
de la sortie du modèle (results.csv dans ce cas, qui est créé automatiquement).

    ```
       {
          "source":{
             "fileformat":"csv",
      "firstlineheader":"true",
      "container":"batchjob",
      "inferschema":"1",
      "filename":"TelcoCustomerData.csv",
      "type":"bluemixobjectstorage"
          },
          "connection":{
             "projectid":"252341ed707d4558b5b2da245e785cd7",
             "userid":"b2d83cf6056e040ddb91ca00a2686c7d3",
             "region":"dallas",
             "authurl":"https://identity.open.softlayer.com",
             "password":"eJ_y9R^OE{j?8Ub!!"
          }
       }
    ```
    {: codeblock}

    **Connexion en sortie**

    ```
       {
          "target":{
             "fileformat":"csv",
      "firstlineheader":"true",
      "container":"batchjob",
      "inferschema":"1",
      "filename":"result.csv",
      "type":"bluemixobjectstorage"
          },
          "connection":{
             "projectid":"252341ed707d4558b5b2da245e785cd7",
             "userid":"b2d83cf6056e040ddb91ca00a2686c7d3",
             "region":"dallas",
             "authurl":"https://identity.open.softlayer.com",
             "password":"eJ_y9R^OE{j?8Ub!!"
          }
       }
    ```
    {: codeblock}

    **Spark Connection** : les données d'identification du service Spark se trouvent sur l'onglet Données d'identification pour le service du tableau de bord du
service Bluemix Spark.

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

5.  Cliquez sur **Sauvegarder**.

Le résultat du pronostic est enregistré dans un fichier .csv dans IBM Object Storage. Un exemple de lignes figure ci-dessous.

Aperçu du fichier d'entrée :

```
customerID,gender,SeniorCitizen,Partner,Dependents,tenure,PhoneService,MultipleLines,InternetService,OnlineSecurity,OnlineBackup,DeviceProtection,TechSupport,StreamingTV,StreamingMovies,Contract,PaperlessBilling,PaymentMethod,MonthlyCharges,TotalCharges,Churn
7590-VHVEG,Female,0,Yes,No,1,No,No phone service,DSL,No,Yes,No,No,No,No,Month-to-month,Yes,Electronic check,29.85,29.85,No
5575-GNVDE,Male,0,No,No,34,Yes,No,DSL,Yes,No,Yes,No,No,No,One year,No,Mailed check,56.95,1889.5,No
3668-QPYBK,Male,0,No,No,2,Yes,No,DSL,Yes,Yes,No,No,No,No,Month-to-month,Yes,Mailed check,53.85,108.15,Yes
```
{: codeblock}

Output file preview:

```
InternetService, Contract, tenure, MonthlyCharges, Churn
Fiber optic, Month-to-month, 2, 70.7, 1
DSL, Two year, 58, 59.9, 0
DSL, Month-to-month, 1, 30.2, 1
DSL, Month-to-month, 17, 64.7, 1
DSL, Month-to-month, 13, 76.2, 0
DSL, Month-to-month, 25, 69.5, 1
Fiber optic, Month-to-month, 8, 80.65, 1
No, One year, 52, 20.4, 0
Fiber optic, Two year, 64, 111.6, 0
Fiber optic, Month-to-month, 1, 79.35, 1
```
{: codeblock}


## Obtention des détails du déploiement

Vous pouvez vérifier le statut et les paramètres associés au modèle déployé.

1. Accédez à l'onglet Déploiements du tableau de bord d'IBM® Watson™ Machine Learning.

2. Dans le menu ACTIONS, sélectionnez Afficher les détails.


## Suppression d'un déploiement par lots

Si vous n'en avez plus besoin, vous pouvez supprimer le déploiement à l'aide d'une requête similaire à l'exemple suivant.

1. Accédez à l'onglet Déploiements du tableau de bord d'IBM® Watson™ Machine Learning.

2. Dans le menu ACTIONS, sélectionnez Supprimer.
