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

# Système d'apprentissage continu <span class='tag--beta'>bêta</span>

Le système d'apprentissage continu d'IBM® Watson™ Machine Learning permet de surveiller les performances du modèle de manière automatique et d'effectuer un ré-entraînement et un redéploiement afin de garantir la qualité des prévisions.

**Scenario name** : Meilleur médicament pour la sélection de traitement du coeur.

**Scenario description** : Une société biomédicale qui produit des médicaments pour le coeur souhaite déployer un modèle qui sélectionne le meilleur médicament pour
le traitement du coeur. Lorsque de nouvelles informations sont collectées sur l'efficacité d'un médicament, une mise à jour du modèle doit être envisagée. Un spécialiste des données prépare un
modèle prédictif et le partage avec vous (le développeur). Votre tâche est de déployer le modèle, de définir une configuration d'apprentissage et d'exécuter une itération d'apprentissage pour
évaluer le modèle, le ré-entraîner et le redéployer.

## Utilisation de l'exemple de modèle

1. Accédez à l'onglet Exemples du tableau de bord IBM® Watson™ Machine Learning.

2. Dans la section Exemples de modèles, recherchez la vignette Sélection de médicaments pour le coeur et cliquez sur le bouton Ajouter le modèle (+).

Vous verrez alors s'afficher l'exemple de modèle Sélection de médicaments pour le coeur dans la liste des modèles disponibles sur l'onglet Modèles.


## Définissez le système d'apprentissage continu pour le modèle publié

1.  Accédez à l'onglet Modèles du tableau de bord d'IBM® Watson™ Machine Learning.

2.  Dans le menu **Actions**, cliquez sur **View Details**.

3.  Faites défiler la liste jusqu'à **Retraining Details** et appuyez sur **Edit**.

4.  Vous devez fournir les informations suivantes :

    **Feedback Connection** : Informations relatives à Db2 Warehouse on Cloud, qui seront utilisées comme entrées (données des commentaires en retour) pour
l'évaluation du modèle et le ré-entraînement.
    
    ```
    {
        "connection":{
            "username": "dash102204",
            "host": "awh-yp-small02.services.dal.bluemix.net",
            "password": "NweTlYwPY6cu",
            "db": "BLUDB"
        },
   "source":{
            "type": "dashdb",
            "tablename": "DRUG_FEEDBACK_DATA"
        }
    }
    ```
    {: codeblock}

    Utilisez les instructions suivantes pour préparer le tableau `DRUG_FEEDBACK_DATA` dans Db2 Warehouse on Cloud.
    - Créez une instance [Db2 Warehouse on Cloud Service](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/) (un plan d'entrée est offert).
    - Créez le tableau **DRUG_FEEDBACK_DATA** dans **Db2 Warehouse on Cloud**.
      + Téléchargez le
fichier [drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv) depuis le référentiel Git.
      + Cliquez sur **Open the console** pour commencer avec l'icône **Db2 Warehouse on Cloud**.
      + Sélectionnez **Load Data** et le type de chargement **Desktop**.
      + **Faîtes glisser et déposez** le fichier téléchargé auparavant et appuyez sur **Next**.
      + Sélectionnez **Schema** pour importer les données et cliquez sur **New Table**.
      + Ecrivez un nom pour **new table** puis cliquez sur **Next** pour terminer l'importation des données.
      + Utilisez `;` comme **séparateur de zone**.
      + Cliquez sur **Suivant** pour créer une table avec les données téléchargées.

    **Remarque** : vous pouvez ajouter de nouveaux enregistrements de feedback à la base de données à l'aide de ce
[noeud final d'API REST](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback)

    **Minimal Data Size** : nombre minimal d'enregistrements dans l'ensemble de données de commentaires pour commencer l'évaluation du modèle (partie de l'itération
d'apprentissage).

    ```
    20
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

    **Thresholds**: valeur seuil qui déclenchera le processus de ré-entraînement (si le calcul s'effectue durant l'évaluation, l'indicateur est inférieur au seuil)
    ```
    0.8
    ```

    **Automatically deploy the retrained model** : déployer le modèle re-entraîné si la qualité est meilleure (selon l'indicateur) que celle qui est actuellement déployée.
5.  Cliquez sur **Set up**.


## Exécutez l'itération du système d'apprentissage continu

Dans le cadre de l'itération, le modèle sera évalué. Si la précision évaluée est inférieure au modèle seuil spécifié, un ré-entraînement sera déclenché. Deux jeux de données,
l'entraînement et les commentaires, sont utilisés pour le ré-entraînement et l'évaluation.

1. Pour démarrer une nouvelle itération, sur le formulaire **Details** du modèle, sur l'onglet **Monitor**, cliquez sur **Evaluate**.

3. Pour vérifier les résultats de l'itération, consultez la table Evaluation Events ou la vue de graphique. Vous y trouverez des informations sur la qualité du modèle calculée sur la base
des commentaires (surveillance) et sur la qualité des modèles ré-entraînés (nouvelle version de modèle créée et évaluée).

4. Pour afficher la liste des modèles entraînés automatiquement et leur qualité, accédez à Version History, au bas de l'onglet Overview (View Details -> Overview).
