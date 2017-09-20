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

# API de service


Le service Machine Learning est un ensemble d'API REST qui peut être appelé à partir de n'importe quel langage de programmation et permet l'intégration d'analyses développées par Data
Science Experience dans vos applications. Liez vos applications Bluemix à l'instance de service Machine Learning et générez les analyses prédictives dont vos applications ont besoin pour offrir aux utilisateurs une meilleure valeur ajoutée. Gérez
des modèles dans le [tableau de bord d'administration](pm_service_ui_spark.html) et utilisez ce dernier pour créer des déploiements en ligne, par lots ou en flux intégrés à vos
applications.

Développez des applications vis à vis de fichiers Data Science Experience (modèles Spark et Python) déployés sur une instance de service via les puissantes [API REST](https://watson-ml-api.mybluemix.net/):

*  Extrayez les métadonnées d'un modèle prédictif spécifique
*  Déployez des modèles et gérez les modèles déployés
    *  Déploiement en ligne (évaluation)
    *  Déploiement par lots (compatible avec Db2 Warehouse on Cloud)
    *  Déploiement en flux (compatible avec IBM MessageHub)
*  Extrayez les métadonnées d'un déploiement spécifique
*  Générez des analyses prédictives en soumettant des requêtes de score aux modèles déployés

Reportez-vous aux sections suivantes pour obtenir des exemples d'utilisation d'API REST :

*  [Déploiement en ligne et évaluation](pm_service_api_spark_online.html)
*  [Déploiement par lots avec Db2 Warehouse on Cloud](pm_service_api_spark_batch.html)
*  [Déploiement en flux à l'aide de MessageHub](pm_service_api_spark_streaming.html)
