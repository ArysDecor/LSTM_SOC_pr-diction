# Estimation du State of Charge (SOC) par Intelligence Artificielle

Ce projet vise à estimer l'état de charge (State of Charge - SOC) d'une batterie en utilisant des techniques d'apprentissage profond (Deep Learning). Deux approches distinctes sont implémentées et comparées : un Perceptron Multicouche (MLP) et un réseau Récurrent à Mémoire Court et Long Terme (LSTM).

## 📂 Structure du Projet

Le projet est organisé autour de deux notebooks Jupyter principaux, chacun dédié à une architecture de modèle spécifique, et d'un jeu de données.

*   **`Estimation_SOC_MLP.ipynb`** : Notebook pour l'entraînement et l'évaluation du modèle **MLP** (Multi-Layer Perceptron). Ce modèle utilise une fenêtre temporelle "aplatie" pour prédire le SOC.
*   **`Estimation_SOC_LSTM.ipynb`** : Notebook pour l'entraînement et l'évaluation du modèle **LSTM** (Long Short-Term Memory). Ce modèle exploite la nature séquentielle des données temporelles pour une estimation plus robuste.
*   **`battery_data_csv_forEstimation.csv`** : Le fichier CSV contenant les données brutes de capteurs (Courant, Tension, Température) et le SOC cible.

## 📊 Données

Le dataset contient des enregistrements temporels des paramètres de la batterie :
*   **Current** (Courant)
*   **Voltage** (Tension)
*   **Temperature** (Température)
*   **SOC** (State of Charge - Cible à prédire)

Un prétraitement est appliqué dans chaque notebook pour normaliser ces données (Mise à l'échelle MinMax entre 0 et 1) et les structurer en séquences (fenêtres glissantes) adaptées à l'apprentissage supervisé.

## 🚀 Installation et Utilisation

Les notebooks sont conçus pour être autonomes (par exemple sur Google Colab ou Jupyter Lab local).

### 1. Pré-requis
Une cellule d'installation automatique des dépendances est incluse au début de chaque notebook. Elle installe :
*   `tensorflow`
*   `pandas`
*   `numpy`
*   `matplotlib`
*   `seaborn`
*   `scikit-learn`

### 2. Exécution
1.  Ouvrez l'un des notebooks (`Estimation_SOC_MLP.ipynb` ou `Estimation_SOC_LSTM.ipynb`).
2.  Exécutez la **première cellule** pour installer les bibliothèques nécessaires.
3.  **IMPORTANT** : Une fois l'installation terminée, **redémarrez le noyau (Kernel)** de votre environnement (Menu `Kernel` > `Restart Kernel`) pour prendre en compte les nouvelles installations.
4.  Exécutez toutes les cellules restantes (Menu `Run` > `Run All` ou exécution cellule par cellule).

## 🧠 Modèles et Architecture

### MLP (Multi-Layer Perceptron)
*   **Entrée** : Fenêtre de temps fixe, aplatie en un vecteur 1D.
*   **Architecture** : Couches Denses (Fully Connected) avec activation ReLU et Dropout pour la régularisation.
*   **Sortie** : Activation **Sigmoïde** pour garantir une estimation strictement bornée entre 0 et 1 (SOC).

### LSTM (Long Short-Term Memory)
*   **Entrée** : Séquence temporelle 3D (Samples, TimeSteps, Features).
*   **Architecture** : Couches LSTM permettant de capturer les dépendances temporelles à long terme, suivies de couches Denses.
*   **Sortie** : Activation **Sigmoïde**.

## 📈 Résultats et Évaluation

Les notebooks génèrent automatiquement :
*   Des courbes de perte (Loss) pour surveiller l'entraînement.
*   Des graphiques comparatifs entre le **SOC Réel** et le **SOC Estimé** sur un jeu de test.
*   Des métriques de performance précises :
    *   **MAE** (Mean Absolute Error)
    *   **RMSE** (Root Mean Squared Error)
    *   **R²** (Coefficient de détermination)

L'utilisation de l'activation **Sigmoïde** en sortie permet de respecter les contraintes physiques du SOC (0% à 100%). L'entraînement sur 50 époques assure une bonne convergence.

## 🛠 Auteur
Projet réalisé dans le cadre de l'estimation de SOC par IA.
