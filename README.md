Problem:

Regression problem, we want to predict the value of the crude oil price for the nexte 5 days based on data collected on 30 years.

Dataset:

I use the dataset that I downloaded from https://datahub.io/ for daily and weekly frequencies. For daily frequency this dataset contains 8501 data points and 1762 points for weekly frequency for time period from 01/02/1986 until 09/23/2019. 

Mapping of th eproject:

1/We want to use ARIMA model to make predictions on 5 days crude oil price

2/We compare ARIMA model with LSTM-CNN (encoder CNN and decoder LSTM: ResNet + one layer of LSTM) to make predictions

3/We use transformers and state of art technology to overcome the results of the related paper.

potential 4/ We use single LSTM

Measures used to evaluate performance: 

MAPE (mean absolute percentage error), la moyenne arithméatique des pourcentages d'erreur absolue.


Sources:

Documentation: https://american-cse.org/csci2022-ieee/pdfs/CSCI2022-2lPzsUSRQukMlxf8K2x89I/202800a089/202800a089.pdf (research paper on time series forecasting)


Documentations et point sur les méthodes utilisées:

Préparation des séries temporelles pour les réseau de neurones:

Dans les donnée d'entrainement
les x_train_value sont: les x dernière valeurs avant une prédiction, d'une taiolle fixée loopback
les y_train_labels: une liste de taille fixée horizon que l'on souhaite prédire

Fonctionnement du CNN-LSTM:

    Division en sous-séquences : Chaque séquence de données est divisée en sous-séquences plus petites pour permettre au CNN de capturer des informations locales. Par exemple, si une séquence contient 10 étapes temporelles, elle peut être divisée en sous-séquences de 2 étapes temporelles chacune.

    Interprétation par le CNN : Le modèle CNN est configuré pour interpréter chaque sous-séquence, en s'attendant à recevoir 2 étapes temporelles par sous-séquence avec une seule caractéristique (ou canal). Le CNN extrait des caractéristiques pertinentes pour chaque sous-séquence.

    Application de CNN sur chaque sous-séquence : Les sous-séquences sont présentées au modèle CNN, et pour chaque sous-séquence, le CNN extrait des informations locales, capturant les détails et les motifs spécifiques à ces deux étapes temporelles.

    Wrap avec TimeDistributed : Le modèle CNN est enveloppé dans des couches TimeDistributed, une couche spécifique utilisée dans les réseaux récurrents pour appliquer des opérations sur chaque étape temporelle de manière indépendante. Ainsi, le modèle CNN est appliqué à chaque sous-séquence individuellement.

    Interprétation par le LSTM : Les sorties du CNN pour chaque sous-séquence sont ensuite interprétées par la couche LSTM. Le LSTM peut comprendre les relations séquentielles entre les sorties du CNN et apprendre les dépendances temporelles plus longues.

    Prédiction : En fin de compte, après avoir interprété toutes les sous-séquences avec le CNN et le LSTM, le modèle combine ces informations pour générer une prédiction finale pour les étapes temporelles suivantes.