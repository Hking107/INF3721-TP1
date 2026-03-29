### **README.md : Guide d'Inférence pour le Modèle k-NN**

# Guide d'Utilisation du Modèle

Ce document détaille les étapes nécessaires pour prédire la classe de revenu (`Income_Group`) d'un pays à partir de ses indicateurs économiques de la Banque Mondiale.

## 1. Préparation des Données d'Entrée
Le vecteur d'entrée doit contenir uniquement les colonnes présentes dans `dataset_traite.csv`. 
- **Ordre des colonnes** : Doit être identique à celui utilisé lors de l'entraînement.
- **Valeurs manquantes** : Si des indicateurs sont absents, utilisez la médiane de l'ensemble d'entraînement pour les combler.

## 2. Standardisation obligatoire
Le modèle k-NN est extrêmement sensible aux échelles. Vous **devez** transformer vos nouvelles données avec le scaler ajusté sur le jeu d'entraînement :
```python
# X_new est votre DataFrame de nouvelles données
X_new_scaled = scaler.transform(X_new)
```

## 3. Paramètres du Modèle
- **Algorithme** : K-Nearest Neighbors (implémentation personnalisée).
- **Distance** : Manhattan ($L1$) - recommandée pour sa capacité à mieux séparer les classes dans cet espace de haute dimension.
- **K (Voisins)** : 12.

## 4. Sortie du Modèle
Le modèle retourne une étiquette textuelle parmi :
- `Low income` (0)
- `Lower middle income` (1)
- `Upper middle income` (2)
- `High income` (3)