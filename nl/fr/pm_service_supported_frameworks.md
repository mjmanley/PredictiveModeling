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

# Structures d'apprentissage automatique prises en charge

Le service IBM Watson Machine Learning prend en charge les structures suivantes pour le développement et la validation de modèles dans le cadre de la gestion du cycle de vie des modèles.


## Spark MLlib
Une prise en charge de Spark MLlib existe pour le service Déploiement en ligne, par lots (bêta), en flux (bêta) et évaluation de Watson Machine Learning. Seules certaines versions et seuls
certains environnements d'exécution sont pris en charge.

### Versions prises en charge
*  Spark 2.0

### Restrictions :

  *  Seuls les modèles de classification et de régression sont pris en charge.
  *  Les modèles qui contiennent des références à des transformateurs personnalisés, à des classes et à des fonctions définies par l'utilisateur ne sont pas pris en charge.
  * Le noeud final "schema" renvoyé durant la demande de déploiement de modèle scikit-learn n'est pas pris en charge à ce stade.
  *  La prise en charge des lots et des flux pour les modèles Spark en est actuellement à la version bêta. Si vous souhaitez participer, inscrivez-vous sur la
[liste d'attente](https://www.ibm.biz/mlwaitlist) !
  * Le système d'apprentissage continu pour les modèles Spark en est à la version bêta. Si vous souhaitez participer, inscrivez-vous sur la
[liste d'attente](https://www.ibm.biz/mlwaitlist) !

## Scikit-learn
Une prise en charge de scikit-learn existe pour le service Déploiement en ligne et évaluation de Watson Machine Learning. Seules certaines versions et seuls certains environnements
d'exécution sont pris en charge.

### Versions prises en charge

- Anaconda 4.2.x pour environnement d'exécution Python 3.5
- Scikit-Learn 0.17

### Environnement d'exécution Python

L'environnement d'exécution Python pour les modèles qui ont besoin d'être déployés à l'aide du service Déploiement en ligne et évaluation de WML est Python 3.5.

Dans certains cas, où les modèles ont été créés dans l'environnement d'exécution Python 2.7, le déploiement peut échouer en raison d'une incompatibilité entre Python2.7 et Python3.5.

### Package Python pris en charge

Pour obtenir une liste des packages Python pris en charge par le service Déploiement en ligne et évaluation de WML, [cliquez ici](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35).

### Restrictions

Des restrictions existent qui peuvent inclure toutes ou partie des limitations suivantes :

* Seuls les modèles de classification et de régression sont pris en charge.
* Les modèles peuvent contenir des références aux packages (et versions de package) pris en charge par Anaconda 4.2.x pour environnement d'exploitation Python 3.5.
* Le noeud final "schema" renvoyé durant la demande de déploiement n'est pas implémenté.
* La probabilité de la prévision n'est pas renvoyée comme réponse à la demande d'évaluation à ce stade.
* Les modèles nécessitant Pandas Dataframe comme type d'entrée pour l'API "predict()" ne sont pas pris en charge.
* Les modèles qui contiennent des références à des transformateurs personnalisés, à des classes et à des fonctions définies par l'utilisateur ne sont pas pris en charge.

## XGBoost <span class='tag--beta'>Béta</span>
XGBoost est pris en charge pour le service Déploiement en ligne et évaluation de Watson Machine Learning. Seules certaines versions et seuls certains environnements d'exécution sont pris en
charge.

### Versions prises en charge

- XGBoost 0.6
- Anaconda 4.2.x pour environnement d'exécution Python 3.5
- Scikit-Learn 0.17

### Environnement d'exécution Python

L'environnement d'exécution Python pour les modèles qui ont besoin d'être déployés à l'aide du service Déploiement en ligne et évaluation de WML est Python 3.5.

Dans certains cas, où les modèles ont été créés dans l'environnement d'exécution Python 2.7, le déploiement peut échouer en raison d'une incompatibilité entre Python2.7 et Python3.5.

### Package Python pris en charge

Pour obtenir une liste des packages Python pris en charge par le service Déploiement en ligne et évaluation de WML,
[cliquez ici](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35).

### Restrictions

Des restrictions existent qui peuvent inclure toutes ou partie des limitations suivantes :
* Une prise en charge de XGBoost est actuellement disponible pour les modèles créés à l'aide des encapsuleurs Scikit-Learn de XGBoost, à savoir xgboost.sklearn.XGBClassifier et
xgboost.sklearn.XGBRegressor.
* Les modèles peuvent contenir des références aux packages (et versions de package) pris en charge par Anaconda 4.2.x pour environnement d'exploitation Python 3.5.
* Le noeud final "schema" renvoyé durant la demande de déploiement n'est pas implémenté.
* La probabilité de la prévision n'est pas renvoyée comme réponse à la demande d'évaluation à ce stade.
* Les modèles contenant des références à des transformateurs personnalisés, à des classes et à des fonctions définies par l'utilisateur ne sont pas pris en charge.

## SPSS Modeler

Une prise en charge des flux SPSS Modeler existe pour le service Déploiement en ligne, par lots et évaluation de Watson Machine Learning. Seules certaines versions et seuls certains
environnements d'exécution sont pris en charge.

### Versions prises en charge

*  SPSS Modeler 17.1
*  SPSS Modeler 18.0

### Restrictions

Les restrictions suivantes existent pour les flux SPSS Modeler :

*  Lorsqu'une branche d'évaluation est préparée pour être utilisée dans une évaluation en temps réel, les données d'entrée dans la demande d'évaluation doivent remplacer le noeud source conçu dans la branche d'évaluation et la sortie de l'analyse prédictive doit être renvoyée dans le flux de réponse (afin de remplacer le noeud terminal dans la conception de branche d'évaluation).
*  La branche d'évaluation étant préparée pour une exécution en temps réel dans Bluemix, elle ne peut pas nécessiter de connexion avec un service externe. Par exemple, une conception de branche d'évaluation IBM Analytical Decision Management ne peut pas contenir de références à des règles ou des modèles stockés dans un référentiel IBM SPSS Collaboration and
Deployment Services.
*  L'exécution d'une branche d'évaluation pour l'évaluation en temps réel dans Bluemix ne peut pas nécessiter de connexion avec un service externe. Par exemple, vous ne pouvez pas effectuer de déploiement et d'évaluation par rapport à des algorithmes de modèle qui nécessitent un serveur IBM SPSS
Analytic Server et un magasin de données Apache Hadoop en temps réel.
*  Machine Learning prend en charge les scripts Python imbriqués dans Modeler. Quelques restrictions sont présentes en raison de la méthode utilisée pour le traitement
des flux avant leur exécution dans Machine Learning. En règle générale, si un utilisateur choisit de contrôler l'exécution du flux, il fait référence au noeud terminal de la branche. Pour Machine Learning, lorsque nous traitons le flux, nous identifions les noeuds
issus de JSON qui seront remplacés, puis effectuons le remplacement avant l'exécution
du flux. Cela provoque l'échec du flux dans le script car l'entrée référencée et les noeuds d'exportation n'existent plus. La solution consiste à utiliser l'ID d'un autre noeud afin d'identifier de manière unique la branche lors de l'exécution. Cela garantit que le flux s'exécute conformément à sa définition dans le script Python imbriqué.

## Informations supplémentaires

Pour obtenir plus d'informations sur la prise en charge actuelle des modèles prédictifs entraînés par IBM SPSS Analytic Server, voir la section
[SPSS Analytic Server](https://www.ibm.com/support/knowledgecenter/SSWLVY) d'[IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/).
