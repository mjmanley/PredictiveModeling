---

copyright:
  years: 2016, 2017
lastupdated: "2017-09-07"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à Watson Machine Learning
{: #WMLgettingstarted}

Utilisez le service IBM® Watson™ Machine Learning pour intégrer des analyses prédictives à vos applications. Les spécialistes des données utilisent l'apprentissage automatique pour
développer des modèles prédictifs alors que les développeurs l'utilisent pour créer des applications permettant de prendre des décisions plus intelligentes, de résoudre des problèmes complexes
et d'améliorer les résultats des utilisateurs.
{: shortdesc}

## Conditions requises

Pour utiliser Watson Machine Learning, vous devez créer dans le catalogue Bluemix [l'instance
de service ici](https://console.bluemix.net/catalog/services/ibm-watson-machine-learning/).

## Procédure

1. [Créez et stockez un modèle](pm_custom_models.html).
2. [Déployez un modèle](pm_service_api_spark_online.html).
3. Utilisez le `noeud final d'évaluation` du modèle déployé dans votre application pour [obtenir des prévisions.](pm_service_api_spark_building.html)

## A propos de Watson Machine Learning

Le service Watson Machine Learning est un ensemble d'API REST qui peut être appelé à partir de n'importe quel langage de programmation.

Le service Watson Machine Learning est centré sur le déploiement, mais notez qu'IBM SPSS Modeler ou Data Science Experience sont requis pour la création et l'utilisation de modèles
et de pipelines. SPSS
Modeler et Data Science Experience (qui exploite Spark MLlib et Python scikit-learn)
proposent tous deux diverses méthodes de modélisation issues de l'apprentissage automatique, de l'intelligence artificielle et des statistiques.

## Liens connexes

Prêt à commencer ? Pour créer une instance d'un service ou lier une application, voir
[Utilisation du service avec des modèles Spark et Python](using_pm_service_dsx.html) ou
[Utilisation du service avec des modèles SPSS](using_pm_service.html).

Si vous souhaitez explorer l'API, veuillez consulter [API du service Machine Learning pour les modèles Spark et Python](pm_service_api_spark.html) ou [API du service Machine Learning pour les modèles IBM SPSS Modeler](pm_service_api_spss.html).

Pour plus d'informations sur SPSS Modeler et les algorithmes de modélisation qu'il utilise, reportez-vous à la documentation du site [IBM
Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7).

Pour plus d'informations sur IBM Data Science Experience et les algorithmes de modélisation qu'il propose, accédez au site
[https://datascience.ibm.com](https://datascience.ibm.com).
