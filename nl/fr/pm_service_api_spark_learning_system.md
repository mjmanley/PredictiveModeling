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

# Système d'apprentissage continu <span class='tag--beta'>Beta</span>

Le système d'apprentissage continu permet un contrôle automatique des performances du modèle, un ré-entraînement et des redéploiements afin de garantir la qualité des prévisions.


**Scenario name** : Meilleur médicament pour la sélection de traitement du coeur.

**Scenario description** : un société biomédicale qui produit des médicaments pour le coeur souhaite développer un modèle qui sélectionne le meilleur médicament pour le
traitement du coeur. Lorsque de nouvelles informations sont collectées sur l'efficacité d'un médicament, une mise à jour du modèle doit être envisagée. Un spécialiste des données a développé un modèle prédictif et le partage avec vous (le développeur). Votre
tâche est de déployer le modèle, de définir une configuration d'apprentissage et d'exécuter l'itération d'apprentissage pour évaluer, ré-entraîner et redéployer le modèle.

**Remarque **: vous pouvez également jouer avec l'exemple de
[dossier](https://apsportal.ibm.com/analytics/notebooks/a97cde0b-5bb8-436a-ae82-83e96adc45e0/view?access_token=6baf4c722e452836f7b505205bc96d9a24b9333ee9b5c39453f6d7751987f798)
Python, qui crée un exemple de modèle, configure le système d'apprentissage et exécute ensuite l'itération d'apprentissage.

## Utilisation de l'exemple de modèle

1. Accédez à l'onglet **Exemples** du tableau de bord d'IBM® Watson™ Machine Learning.

2. Dans la section **Exemples de modèles**, recherchez la vignette Sélection de médicaments pour le coeur et cliquez sur l'icône **Ajouter le modèle**
(+).

Vous verrez alors s'afficher l'exemple de modèle Sélection de médicaments pour le coeur dans la liste des modèles disponibles sur l'onglet Modèles.

## Génération du jeton d'accès

Générez un jeton d'accès à partir de l'ID et du mot de passe utilisateur affichés dans l'onglet Données d'identification pour le service de l'instance de service IBM Watson Machine Learning.

Exemple de requête :

```
curl --basic --user <username>:<password> https://ibm-watson-ml.mybluemix.net/v3/identity/token
```
{: codeblock}

Exemple de sortie :

```
{"token":"**********"}
```
{: codeblock}

Utilisez la commande de terminal suivante pour affecter votre valeur de jeton au jeton de la variable d'environnement :

```
token="<token_value>"
```
{: codeblock}

## Utilisation de modèles publiés

Utilisez l'appel API suivant pour obtenir les détails de votre instance, par exemple :

* `url` des modèles publiés
* `url` des déploiements
* informations sur l'utilisation

Exemple de requête :

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer  $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}
```
{: codeblock}

Exemple de sortie :

```
{
   "metadata":{
      "guid":"360c510b-012c-4793-ae3f-063410081c3e",
      "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e",
      "created_at":"2017-08-04T09:15:48.344Z",
      "modified_at":"2017-08-22T08:34:47.759Z"
   },
   "entity":{
      "source":"Bluemix",
      "published_models":{
         "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/published_models"
      },
      "usage":{
         "expiration_date":"2017-09-01T00:00:00.000Z",
         "computation_time":{
            "current":4
         },
         "model_count":{
            "limit":1000,
            "current":2
         },
         "prediction_count":{
            "current":16
         },
         "deployment_count":{
            "limit":1000,
            "current":1
         }
      },
      "plan_id":"0f2a3c2c-456b-40f3-9b19-726d2740b11c",
      "status":"Active",
      "organization_guid":"b0e61605-a82e-4f03-9e9f-2767973c084d",
      "region":"us-south",
      "account":{
         "id":"f52968f3dbbe7b0b53e15743d45e5e90",
         "name":"Umit Cakmak's Account",
         "type":"TRIAL"
      },
      "owner":{
         "ibm_id":"31000292EV",
         "email":"umit.cakmak@pl.ibm.com",
         "user_id":"43e0ee0e-6bfb-48fc-bcd8-d61e40d19253",
         "country_code":"POL",
         "beta_user":true
      },
      "deployments":{
         "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/deployments"
      },
      "space_guid":"4c55eb1c-d6fe-4f0a-9390-35c9a7ecf27a",
      "plan":"standard"
   }
}
```
{: codeblock}


Avec l'`url` **published_models**, utilisez l'appel API suivant pour obtenir les détails du modèle :

Exemple de requête :

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer  $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models
```
{: codeblock}

Exemple de sortie :

```
{  
   "count":1,
   "resources":[  
      {  
         "metadata":{
      "guid":"361d0edb-c5c9-4b8c-b353-d968e7dc0b8d",
            "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/published_models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d",
            "created_at":"2017-08-22T08:34:47.597Z",
            "modified_at":"2017-08-22T08:34:47.691Z"
         },
   "entity":{
      "runtime_environment":"spark-2.0",
            "author":{  

            },
            "name":"Best Heart Drug Selection",
            "label_col":"DRUG",
            "training_data_schema":{  
               "fields":[  
                  {  
                     "metadata":{
      "scale":0,
                        "name":"AGE"
                     },
                     "type":"integer",
                     "name":"AGE",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":0,
                        "name":"SEX"
                     },
                     "type":"string",
                     "name":"SEX",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":0,
                        "name":"BP"
                     },
                     "type":"string",
                     "name":"BP",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":0,
                        "name":"CHOLESTEROL"
                     },
                     "type":"string",
                     "name":"CHOLESTEROL",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":6,
                        "name":"NA"
                     },
                     "type":"decimal(12,6)",
                     "name":"NA",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":6,
                        "name":"K"
                     },
                     "type":"decimal(13,6)",
                     "name":"K",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":0,
                        "name":"DRUG"
                     },
                     "type":"string",
                     "name":"DRUG",
                     "nullable":true
                  }
               ],
               "type":"struct"
            },
            "latest_version":{  
               "url":"https://ibm-watson-ml.mybluemix.net/v2/artifacts/models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d/versions/8dfe9548-57ec-4768-8d3e-6c1e7e5cdfc3",
               "guid":"8dfe9548-57ec-4768-8d3e-6c1e7e5cdfc3",
               "created_at":"2017-08-22T08:34:47.691Z"
            },
            "model_type":"sparkml-model-2.0",
            "deployments":{  
               "count":0,
               "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/published_models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d/deployments"
            },
            "input_data_schema":{  
               "fields":[  
                  {  
                     "metadata":{
      "scale":0,
                        "name":"AGE"
                     },
                     "type":"integer",
                     "name":"AGE",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":0,
                        "name":"SEX"
                     },
                     "type":"string",
                     "name":"SEX",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":0,
                        "name":"BP"
                     },
                     "type":"string",
                     "name":"BP",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":0,
                        "name":"CHOLESTEROL"
                     },
                     "type":"string",
                     "name":"CHOLESTEROL",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":6,
                        "name":"NA"
                     },
                     "type":"decimal(12,6)",
                     "name":"NA",
                     "nullable":true
                  },
                  {  
                     "metadata":{
      "scale":6,
                        "name":"K"
                     },
                     "type":"decimal(13,6)",
                     "name":"K",
                     "nullable":true
                  }
               ],
               "type":"struct"
            }
         }
      }
}
```
{: codeblock}


## Définissez le système d'apprentissage continu pour le modèle publié

Dans cette sous-section, vous apprendrez à configurer le système d'apprentissage continu pour votre modèle.

### Préparation de l'en-tête d'autorisation

Pour préparer l'en-tête d'autorisation qui combine le jeton Watson Machine Learning et les données d'identification d'instance Spark, entrez les informations suivantes :

*  Le jeton d'accès créé à l'étape précédente
*  Les données d'identification du service Spark, que vous pouvez trouver dans l'onglet Données d'identification du service du tableau de bord du service Bluemix Spark. Avant
d'effectuer la demande de déploiement, les données d'identification Spark doivent être codées en base64. Elles sont transmises dans l'en-tête de la demande dans la zone X-Spark-Service-Instance.

   Suivant le système d'exploitation que vous utilisez, vous devez émettre l'une des commandes de terminal suivantes pour effectuer un codage en base64 et l'affecter à la variable
d'environnement.

   Sur le système d'exploitation macOS, utilisez la commande suivante :

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64)
   ```
   {: codeblock}

   Sur les systèmes d'exploitation Microsoft Windows ou Linux, vous devez utiliser le paramètre `--wrap=0` avec la commande `base64` pour effectuer un
codage en base64 :

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64 --wrap=0)
   ```
   {: codeblock}


### Préparez le jeu de données de commentaire

Learning System nécessite une connexion aux données d'entraînement (données utilisées pour l'entraînement du modèle) ainsi qu'aux données de commentaires (données utilisées pour évaluer le
modèle entraîné). Utilisez les instructions ci-dessous pour préparer la table **DRUG_FEEDBACK_DATA** dans **Db2 Warehouse on Cloud**.

- Créez une instance [Db2 Warehouse on Cloud Service](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/) (un plan d'entrée est offert).
- Créez le tableau **DRUG_FEEDBACK_DATA** dans **Db2 Warehouse on Cloud**.
  + Téléchargez le fichier [drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv)
depuis le référentiel Git.
  + Cliquez sur **Open the console** pour commencer avec l'icône **Db2 Warehouse on Cloud**.
  + Sélectionnez **Load Data** et le type de chargement **Desktop**.
  + **Faîtes glisser et déposez** le fichier téléchargé auparavant et appuyez sur **Next**.
  + Sélectionnez **Schema** pour importer les données et cliquez sur **New Table**.
  + Dans la zone **new table**, entrez un nom et cliquez sur **Next**.
  + Utilisez le point-virgule (;) comme **séparateur de zone**.
  + Cliquez sur **Next** pour créer une table avec les données téléchargées.

**Remarque** : vous pouvez ajouter de nouveaux enregistrements de feedback à la base de données à l'aide de ce
[noeud final d'API REST](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback)

### Préparez le contenu de configuration

Pour pouvoir spécifier la configuration d'apprentissage, vous devez utiliser le noeud final suivant :

```
https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_configuration
```
   {: codeblock}


Définissez les valeurs des zones suivantes pour finaliser le contenu :

* `min_feedback_data_size` - il s'agit du nombre minimal d'enregistrements requis dans le jeu de données de commentaires pour démarrer l'itération du système
d'apprentissage continu
* `auto_retrain` [never, always, conditionally] - ce paramètre spécifie quand le processus de ré-entraînement doit être déclenché. [conditionally] déclenchera le
processus de ré-entraînement lorsque la qualité du modèle sera située au-dessous du seuil spécifié.
* `auto_redeploy` [never, always, conditionally] - ce paramètre indique quand le modèle ré-entraîné doit être déployé. [conditionally] déclenchera le redéploiement du
modèle lorsque la qualité du modèle ré-entraîné sera meilleure que celle du modèle déployé en cours.


Exemple de requête :

```
curl -v -X PUT \
    -H "Content-Type:application/json" \
    -H "Authorization: Bearer $token" \
    -H "X-Spark-Service-Instance: $spark_credentials" \
    -d '{
          "definition": {
            "method": "binary",
            "metrics": [
              {
                "name": "areaUnderROC",
        "threshold": 0.8
      }
            ]
          },
          "feedback_data_ref": {
           "connection":{
            "db": "BLUDB",
            "host": "awh-yp-small02.services.dal.bluemix.net",
            "username": "dash102204",
            "password": "NweTlYwPY6cu"
           },
   "source":{
            "tablename": "DRUG_FEEDBACK_DATA",
            "type": "dashdb"
           }
          },
          "min_feedback_data_size": 100,
          "auto_retrain": "conditionally",
          "auto_redeploy": "conditionally",
          "schedule": {
            "expression": "0/15 * * * * ? *",
            "start": "2017-02-01T10:11:12Z",
            "until": "2017-06-01T10:11:12Z"
          },
          "last_training_record": 0
        }' \
    https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_configuration
```

{: codeblock}

Exemple de sortie :
```
{
   "min_feedback_data_size":100,
   "auto_retrain":"conditionally",
   "schedule":{
      "expression":"0/15 * * * * ? *",
      "start":"2017-02-01T10:11:12Z",
      "until":"2017-06-01T10:11:12Z"
   },
   "definition":{
      "method":"binary",
      "metrics":[
         {
            "name": "areaUnderROC",
        "threshold": 0.8
      }
      ]
   },
      "spark_service":{
      "credentials": {
         "tenant_id":"s971-2eeb9ffe2a3090-35c9a7ecf27a",
         "cluster_master_url":"https://spark.bluemix.net",
         "tenant_id_full":"55f1492d-b385-4fdd-b971-2eeb9ffe2a30_4c55eb1c-d6fe-4f0a-9390-35c9a7ecf27a",
         "tenant_secret":"5e7fc568-e94e-4689-b623-fe62e9ceedd2",
         "instance_id":"55f1492d-b385-4fdd-b971-2eeb9ffe2a30",
         "plan":"ibm.SparkService.PayGoPersonal"
      },
         "version":"2.0"
   },
   "feedback_data_ref":{
      "connection":{
         "db":"BLUDB",
         "host":"awh-yp-small02.services.dal.bluemix.net",
         "username":"dash102204",
         "password":"NweTlYwPY6cu"
      },
      "source":{
         "tablename":"DRUG_FEEDBACK_DATA",
         "type":"dashdb"
      }
   },
   "auto_redeploy":"conditionally"
}
```
{: codeblock}

**Remarque **: Dans cet exemple, nous utilisons les valeurs par défaut des paramètres `auto_retrain` et `auto_redeploy`. Vous trouverez
des informations supplémentaires sur ces paramètres ici dans la
[documentation de l'API
REST](http://watson-ml-api.mybluemix.net/#!/Published32Models/put_v3_wml_instances_instance_id_published_models_published_model_id_learning_configuration) du paramètre learning_configuration.

## Exécutez l'itération du système d'apprentissage continu

Pour démarrer l'itération du système d'apprentissage, utilisez la méthode de l'API REST décrite ci-dessous. Dans le cadre de l'itération, le modèle sera évalué. Si la précision évaluée est
inférieure au modèle seuil spécifié, un ré-entraînement sera déclenché. Deux jeux de données - l'entraînement et les commentaires -  sont utilisés pour le ré-entraînement et l'évaluation.

Exemple de requête :

```
curl -X POST --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

Exemple de sortie :

```
The request has been fulfilled and resulted in a new resource being created.
```
{: codeblock}

Pour vérifier le statut de l'itération, émettez la requête suivante :

Exemple de requête :

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

Exemple de sortie :

```
{
   "count":1,
   "resources":[
      {
         "metadata":{
            "guid":"4091f245-0f0b-42c6-aec9-6ab68185c47f",
            "url":"https://ibm-watson-ml-dev.stage1.mybluemix.net/v3/wml_instances/87452a37-6a8f-4d59-bf88-59c66b5463e4/published_models/9894c3d5-e923-4544-9a7c-2fdb3e4d0908/learning_iterations/4091f245-0f0b-42c6-aec9-6ab68185c47f",
            "created_at":"2017-07-07T11:18:46.742Z",
            "modified_at":"2017-07-07T11:18:48.100Z"
         },
   "entity":{
            "stage":"StartingKernel",
            "published_model":{
               "url":"https://ibm-watson-ml-dev.stage1.mybluemix.net/v3/wml_instances/87452a37-6a8f-4d59-bf88-59c66b5463e4/published_models/9894c3d5-e923-4544-9a7c-2fdb3e4d0908",
               "guid":"9894c3d5-e923-4544-9a7c-2fdb3e4d0908"
            },
            "status":"RUNNING",
            "kernel_id":"db56fc3b-a200-4455-aa70-392aa8ae98b3",
            "spark_service":{
               "credentials": {
                  "tenant_id":"s702-faa29053b44952-01f17dcd4c8c",
                  "cluster_master_url":"https://spark.stage1.bluemix.net",
                  "tenant_id_full":"81d716eb-3c8c-40ef-9702-faa29053b449_a2485898-8ed5-43df-8352-01f17dcd4c8c",
                  "tenant_secret":"9f18945c-8e4b-4d2b-8104-f429b27a896d",
                  "instance_id":"81d716eb-3c8c-40ef-9702-faa29053b449",
                  "plan":"ibm.SparkService.PayGoPersonal"
               },
               "version":"2.0"
            }
         }
      },
   ]
}
```
{: codeblock}

Vous pouvez également obtenir la liste des métriques d'évaluation et des valeurs en émettant la requête suivante :

Exemple de requête :

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/evaluation_metrics
```
{: codeblock}

Exemple de sortie :

```
{
  "count": 1,
  "resources": [
    {
      "phase": "training",
      "values": [
        {
          "name": "areaUnderROC",
          "value": 0.94,
          "threshold": 0.8
        }
      ],
      "timestamp": "2017-08-08T10:11:12.000Z",
      "artifactVersionHref": "https://ibm-watson-ml.mybluemix.net/v3/artifacts/models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d/versions/8dfe9548-57ec-4768-8d3e-6c1e7e5cdfc3"
    }
  ]
}
```
{: codeblock}
