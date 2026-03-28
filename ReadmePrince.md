# Classification des Revenus des Pays (Modèle k-NN)


##  Présentation du Projet
L'objectif de ce travail est de prédire la catégorie de revenu d'un pays (**Income_Group**) en se basant sur **1516 indicateurs économiques** fournis par la Banque Mondiale pour l'année 2023. Nous utilisons l'algorithme des **k-Plus Proches Voisins (k-NN)** pour classer les observations.

---

##  Phase 1 : Construction du Jeu de Données
Le dataset a été constitué par l'agrégation automatisée de fichiers CSV :
* **Metadata_Country_API** : Source de la classe cible (`Income_Group`) et du code pays.
* **API_... (Données)** : Source des valeurs de l'année **2023** pour chaque indicateur.
* **Pivotage** : Transformation des données du format "long" vers un format "large" (1 ligne = 1 pays, 1516 colonnes = indicateurs).

---

##  Phase 2 : Gestion Stratégique des Valeurs Manquantes (NaN)
Le traitement des données manquantes a été l'étape la plus critique. Nous avons implémenté une **Imputation Stratifiée (ou Groupée)** basée sur une intuition économique forte.

**Imputation Stratifie**: Elle consiste à remplacer ces valeurs manquantes par la moyenne (ou une autre mesure) calculée uniquement à partir de répondants appartenant à la même sous-population ou « strate ».
-- 
 Contrairement à une imputation globale, cette méthode segmente la population en sous-groupes homogènes (strates), par exemple, le revenu moyen par profession ou le niveau d'éducation par tranche d'âge.


### 1. L'Intuition : Cohérence Économique
Remplacer une donnée manquante par une moyenne mondiale introduirait un biais majeur. 
> **Le principe :** On ne remplace pas un manque de données du Burundi (Low Income) par une moyenne qui inclut la Suisse (High Income). L'imputation doit respecter le profil économique du groupe.

ici ell  vas remplacer une valeur manquante par la moyen par rapport au groupe cet a dire (low income, high income etc)

### 2. Le Choix de la Médiane vs Moyenne
Nous avons privilégié la **médiane par groupe** :
* **Robustesse :** Contrairement à la moyenne, la médiane n'est pas influencée par les pays "atypiques" (*outliers*) au sein d'une catégorie.
* **Fidélité :** Elle offre une valeur centrale plus représentative de la "normalité" d'un groupe de revenu.

On voie ici que la median ne sera pas affecte pas le bruit( valeur dextremite )

### 3. Algorithme d'Imputation Hybride
1. **Niveau 1 (Précision) :** Imputation par la médiane au sein de chaque strate `Income_Group`.
2. **Niveau 2 (Sécurité) :** Imputation par la médiane globale pour les indicateurs totalement absents dans une catégorie entière.
3. **Filtrage des "Not Classified" :** Les pays sans classe définie ont été supprimés car un modèle supervisé nécessite une étiquette réelle pour l'apprentissage.

---

##  Phase 3 : Analyse et Prétraitement
* **Encodage Ordinal** : Transformation de la cible en valeurs numériques hiérarchisées :
  * `Low income` → 0 | `Lower middle income` → 1 | `Upper middle income` → 2 | `High income` → 3.
* **Standardisation (Scaling)** : Application d'un `StandardScaler`. Cette étape est **obligatoire** pour le k-NN afin d'éviter que les variables à grande échelle (ex: PIB) ne dominent le calcul de distance euclidienne.
