# Inférence sur une nouvelle observation

Ce projet utilise un modèle k-NN entraîné dans le notebook `INF3721_TP1_Groupe_1.ipynb`.
Pour prédire la classe `Income_Group` d'un nouveau pays (ou d'une nouvelle observation), suivez les étapes ci-dessous.

### 1. Exécuter le notebook jusqu'à l'entraînement

Dans `INF3721_TP1_Groupe_1.ipynb`, exécutez les cellules dans l'ordre jusqu'à obtenir :
- `X_train_raw` (features d'entraînement non standardisées)
- `scaler` (StandardScaler ajusté sur le train)
- `knn` (modèle entraîné, `k=12`)

Sans ces objets, l'inférence ne peut pas fonctionner.

### 2. Préparer la nouvelle observation

La nouvelle observation doit respecter exactement le même format que les features d'entraînement :
- mêmes colonnes que `X_train_raw`
- même ordre des colonnes
- uniquement des variables numériques

Si des valeurs sont manquantes, appliquez la même logique d'imputation que pendant le prétraitement (médianes utilisées dans le projet).

### 3. Standardiser la nouvelle observation

Le k-NN étant sensible à l'échelle des variables, appliquez le scaler entraîné :

```python
new_observation_scaled = scaler.transform(new_observation_raw.reshape(1, -1))
```

### 4. Faire la prédiction

```python
predicted_income_group = knn.predict(new_observation_scaled)
print(f"Predicted Income Group for the new observation: {predicted_income_group[0]}")
```

La sortie est une classe texte parmi :
- `Low income`
- `Lower middle income`
- `Upper middle income`
- `High income`

### 5. Exemple complet (cellule prête à coller)

```python
import numpy as np

# Vérifier que les objets nécessaires existent déjà
if 'X_train_raw' not in locals() or 'scaler' not in locals() or 'knn' not in locals():
	print("Error: X_train_raw, scaler, or knn model not found. Please run previous cells.")
else:
	# Exemple: observation avec le bon nombre de variables
	# Remplacez les valeurs ci-dessous par vos vraies données
	new_observation_raw = np.array([0] * X_train_raw.shape[1], dtype=float)

	# Standardisation puis prédiction
	new_observation_scaled = scaler.transform(new_observation_raw.reshape(1, -1))
	predicted_income_group = knn.predict(new_observation_scaled)

	print(f"Predicted Income Group for the new observation: {predicted_income_group[0]}")
```
