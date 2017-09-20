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

# Politique de quotas

Le moteur IBM Watson Machine Learning applique des quotas par instance afin de garantir une allocation et une utilisation adéquate des ressources. Ces politiques varient en fonctions
des profils de compte, de l'historique d'utilisation du service et de la disponibilité des ressources. La politique des quotas décrit les limites qui ne sont pas définies par le barème de prix
et qui sont **susceptibles d'être modifiés sans préavis**. 

Les limites de quota de service suivantes sont actives actuellement.

## Utilisation des ressources

Les ressources sont limitées aux valeurs maximales suivantes :

-  **Nombre maximal de modèles publiés** : 200 (forfait gratuit) 1000 (forfaits standard & professionnel)
-  **Taille maximale du modèle Spark ML** : 200 Mo
-  **Nombre maximal de modèles déployés**: 1000 (forfaits standard & professionnel)

**Remarque **: pour comprendre les limites du forfait gratuit, consultez la description du
[forfait gratuit](https://console.bluemix.net/catalog/services/machine-learning) dans le [catalogue Bluemix](https://console.bluemix.net/catalog/).

## Limites des demandes de service

Le nombre de demandes que vous pouvez effectuer par minutes dans certains API est limité. Si votre application nécessite des limites plus élevées, vous devez
[contacter le service d'assistance d'IBM Bluemix](https://support.ng.bluemix.net/) pour augmenter votre quota.

## Demandes de déploiement

Les limites suivantes sont applicables aux demandes d'API de déploiement :

-  **Période** : 60 secondes
-  **Limite par défaut** : 10

## Demandes de prévision en ligne

Les limites suivantes s'appliquent aux demandes de [prévisions en ligne](pm_service_api_spark_building.html) :

-  **Période** : 60 secondes
-  **Limite par défaut** : 500

## Demandes de gestion des ressources

Les limites suivantes s'appliquent aux demandes totales combinées de cette liste :

[Jeton](https://watson-ml-api.mybluemix.net/#/Token) : requêtes post, get, delete, put, patch

[Déploiements](https://watson-ml-api.mybluemix.net/#/Deployments): requêtes post, get, delete, put, patch

-  **Période** : 60 secondes
-  **Limite par défaut** : 100
