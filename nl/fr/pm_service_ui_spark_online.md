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

# Déploiement de modèles en ligne


**Nom du scénario **:  Pronostic de ligne de produits.

**Description du scénario **: une entreprise qui commercialise des équipements de plein air désire construire un modèle pronostiquant l'intérêt des clients pour leur ligne de produits. Un spécialiste des données a développé un modèle prédictif et le partage avec vous (le développeur). Votre tâche consiste à déployer le modèle et à générer des pronostics de l'intérêt des clients en lançant des requêtes de score à partir du modèle déployé.

## Utilisation de l'exemple de modèle

1. Accédez à l'onglet Exemples du tableau de bord IBM® Watson™ Machine Learning.

2. Dans la section Exemples de modèles, recherchez la vignette Pronostics de ligne de produits et cliquez sur le bouton Ajouter le modèle (+).

Vous pouvez observer à présent le modèle Pronostics de ligne de produits dans la liste des modèles disponibles sous l'onglet Modèles.


## Création du déploiement en ligne

1. Accédez à l'onglet Modèles du tableau de bord d'IBM® Watson™ Machine Learning.

2. Dans le menu ACTIONS, sélectionnez Créer un déploiement.

3. Dans le formulaire Créer un déploiement, fournissez un nom, une description et un type en ligne.

4. Appuyez sur le bouton Sauvegarder.

Le déploiement en ligne s'affiche maintenant dans la liste des déploiements disponibles sur l'onglet Déploiements.


## Obtention des détails du déploiement

Vous pouvez vérifier le statut, l'adresse de noeud final d'évaluation (`Scoring Endpoint`) et les paramètres relatifs au modèle déployé.

1. Accédez à l'onglet Déploiements du tableau de bord IBM® Watson™ Machine Learning.

2. Dans le menu ACTIONS, sélectionnez Afficher les détails.

Notez que la valeur de `Scoring Endpoint` est requise pour effectuer des requêtes d'évaluation à l'étape suivante.


## Soumission de requêtes de score

Comme votre noeud final d'évaluation a été créé (`Scoring Endpoint`), vous pouvez maintenant générer des prévisions en effectuant des requêtes de score. Dans ce scénario, des enregistrements client sont transmis au modèle prédictif et un pronostic sur les articles de sport est renvoyé.

Exemple d'en-tête d'enregistrement :

```
GENDER,AGE,MARITAL_STATUS,PROFESSION
```
{: codeblock}

Exemple d'enregistrement :

```
M,27,Single,Professional
F,56,Unspecified,Hospitality
M,45,Married,Retired
```
{: codeblock}

Exemple de requête :

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: Bearer  $token' -d '{"fields": ["GENDER","AGE","MARITAL_STATUS","PROFESSION"],"values": [["M",23,"Single","Student"],["M",55,"Single","Executive"]]}' https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/deployments/{deployment_id}/online
```
{: codeblock}

Exemple de sortie :

```
{
   "fields": ["GENDER",
      "AGE",
      "MARITAL_STATUS",
      "PROFESSION",
      "PROFESSION_IX",
      "GENDER_IX",
      "MARITAL_STATUS_IX",
      "features",
      "rawPrediction",
      "probability",
      "prediction",
      "predictedLabel"
   ],
   "records":[
      [
         "M",
         23,
         "Single",
         "Student",
         6.0,
         0.0,
         1.0,
         [
            0.0,
            23.0,
            1.0,
            6.0
         ],
         [
            5.600716147152702,
            6.482458372136143,
            6.048004170730676,
            0.20929155492307386,
            1.6595297550574055
         ],
         [
            0.2800358073576351,
            0.32412291860680714,
            0.3024002085365338,
            0.010464577746153694,
            0.08297648775287028
         ],
         1.0,
         "Personal Accessories"
      ],
      [
         "M",
         55,
         "Single",
         "Executive",
         3.0,
         0.0,
         1.0,
         [
            0.0,
            55.0,
            1.0,
            3.0
         ],
         [
            6.227653744886563,
            4.325198862164969,
            8.031953760146816,
            1.2319759269281225,
            0.1832177058735289
         ],
         [
            0.3113826872443282,
            0.2162599431082485,
            0.40159768800734086,
            0.06159879634640614,
            0.009160885293676447
         ],
         2.0,
         "Mountaineering Equipment"
      ]
   ]
}
```
{: codeblock}

Nous pouvons constater, par exemple, qu'un cadre âgé de 55 ans est intéressé par les produits de la catégorie Equipements d'alpinisme, tandis qu'un étudiant âgé de 23 ans s'intéresse à la catégorie Accessoires personnels.
