### Projet de Prévision des Prix du Pétrole Brut

#### **Objectif Principal**
Le but est de prédire la valeur du prix du pétrole brut pour les 5 prochains jours, en utilisant des données collectées sur une période de 30 ans.

#### **Ensemble de Données**
J'utilise un jeu de données téléchargé depuis [DataHub](https://datahub.io/) contenant des fréquences quotidiennes et hebdomadaires. La fréquence quotidienne contient 8501 points de données et la fréquence hebdomadaire 1762 points, couvrant la période du 01/02/1986 au 23/09/2019.

#### **Méthodes et Comparaison de Modèles**
1. Utilisation du modèle ARIMA pour prédire le prix du pétrole brut sur 5 jours.
2. Utilisation d'autres méthodes statistiques classiques (SVR, random trees et XGBoost)
3. Comparaison entre le modèle ARIMA et un réseau CNN-LSTM (CNN en tant qu'encodeur et LSTM en tant que décodeur : ResNet + une couche LSTM).
4. Utilisation de techniques d'apprentissage telles que les transformers pour améliorer les résultats par rapport au papier de référence.
5. Évaluation potentielle d'un modèle LSTM simple.

#### **Mesures d'Évaluation**
Utilisation de la MAPE (erreur absolue moyenne en pourcentage), qui représente la moyenne des pourcentages d'erreur absolue.

#### **Déroulement des Analyses**

##### **Préparation des Données pour les Réseaux de Neurones**
- *X_train_value* : Les `x` dernières valeurs avant la prédiction, d'une taille fixée (loopback).
- *y_train_labels* : Une liste de taille fixée représentant l'horizon que l'on souhaite prédire.

##### **Fonctionnement du Modèle CNN-LSTM**
- _Division en Sous-Séquences_ : Chaque séquence est divisée en sous-séquences plus petites pour permettre au CNN de capturer des informations locales.
- _Interprétation par le CNN_ : Le CNN interprète chaque sous-séquence, s'attendant à recevoir un nombre spécifique d'étapes temporelles par sous-séquence.
- _Application de CNN_ : Les sous-séquences sont envoyées au CNN pour extraire des caractéristiques pertinentes.
- _Wrap avec TimeDistributed_ : Le CNN est enveloppé dans des couches TimeDistributed pour appliquer des opérations sur chaque étape temporelle.
- _Interprétation par le LSTM_ : Les sorties du CNN sont interprétées par le LSTM pour apprendre les dépendances temporelles.
- _Prédiction_ : En combinant les informations du CNN et du LSTM, le modèle génère une prédiction finale.

### Source de Référence
La méthodologie est alignée avec la documentation scientifique disponible à [ce lien](https://american-cse.org/csci2022-ieee/pdfs/CSCI2022-2lPzsUSRQukMlxf8K2x89I/202800a089/202800a089.pdf) sur la prévision des séries temporelles.
