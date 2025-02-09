# td3_decentralisation

Code 1 : Logistic Regression (simple et rapide).

Code 2 : Random Forest (robuste pour des ensembles de données complexes).

Code 3 : SVM (idéal pour les frontières de décision claires).

Code 4 : KNN (basé sur la proximité des exemples).


## Résumé des performances des modèles

### **1. Évaluation des modèles**
Les 4 modèles ont été évalués sur le dataset Iris, en utilisant un ensemble de test composé de 30 échantillons. Voici les résultats pour chaque modèle :

| Modèle            | Précision globale | Matrice de confusion                          | F1-score moyen |
|--------------------|-------------------|-----------------------------------------------|----------------|
| Régression Logistique (Code_1.py) | 1.00             | `[[10, 0, 0], [0, 9, 0], [0, 0, 11]]`       | 1.00           |
| Random Forest (Code_2.py)         | 1.00             | `[[10, 0, 0], [0, 9, 0], [0, 0, 11]]`       | 1.00           |
| SVM (Code_3.py)                   | 1.00             | `[[10, 0, 0], [0, 9, 0], [0, 0, 11]]`       | 1.00           |
| KNN (Code_4.py)                   | 1.00             | `[[10, 0, 0], [0, 9, 0], [0, 0, 11]]`       | 1.00           |

---

### **2. Analyse détaillée**
#### Précision globale :
- Tous les modèles ont obtenu une précision globale de **100%**, ce qui signifie que chaque modèle a correctement classé les 30 échantillons de l'ensemble de test.

#### Matrice de confusion :
- La matrice de confusion montre que :
  - **Setosa** (10 échantillons), **Versicolor** (9 échantillons), et **Virginica** (11 échantillons) ont été correctement classifiés sans aucune erreur pour chaque modèle.

#### Rapport de classification :
- Chaque classe (`Setosa`, `Versicolor`, `Virginica`) a atteint une **précision**, un **rappel**, et un **F1-score** de **1.00**.
- Les moyennes macro et pondérées confirment également cette performance parfaite.

---

### **3. Explication des modèles**
1. **Régression Logistique (Code_1.py)** :
   - Modèle simple basé sur la séparation linéaire des classes.
   - Convient bien pour des datasets bien séparés comme Iris.

2. **Random Forest (Code_2.py)** :
   - Modèle basé sur des ensembles d'arbres de décision.
   - Robuste et performant, même sur des problèmes non linéaires.

3. **SVM (Code_3.py)** :
   - Modèle utilisant un noyau RBF pour séparer les classes.
   - Idéal pour des frontières de décision complexes.

4. **KNN (Code_4.py)** :
   - Modèle basé sur les plus proches voisins.
   - Performance dépendante du choix du nombre de voisins.

---

### **4. Conclusion**
- Tous les modèles se comportent parfaitement sur le dataset Iris en raison de la simplicité de ce dernier et de la séparation claire entre les classes.
- Dans des contextes plus complexes, les performances des modèles peuvent varier selon la nature des données. Par exemple :
  - La **Régression Logistique** pourrait échouer si les classes ne sont pas linéairement séparables.
  - Le **KNN** pourrait être sensible aux données bruitées.


# Question 2
![image](https://github.com/user-attachments/assets/71fbb305-eac9-4bbb-a18f-cee2c7255d05)

Le modèle agrégé, basé sur un consensus des prédictions de 4 modèles distincts (Régression Logistique, Random Forest, SVM, et KNN), a obtenu une précision de 100% sur l'ensemble de test du dataset Iris.

## Points forts :
### Robustesse : 
En combinant plusieurs modèles, le consensus permet de corriger les erreurs potentielles de modèles individuels.
Performance : Le vote majoritaire est une méthode simple et efficace pour agréger les prédictions.
### Limites :
Le dataset Iris est relativement simple, ce qui explique les performances parfaites. Sur des datasets plus complexes, cette méthode devra être testée pour vérifier sa robustesse.

# Question 3 

#### **Objectif :**
Introduire un système de **pondération dynamique** pour améliorer la précision et la robustesse d'un modèle agrégé, basé sur le consensus des prédictions de plusieurs modèles.

---

#### **Description du Code :**
Ce code interroge quatre modèles distincts (Régression Logistique, Random Forest, SVM, KNN), regroupe leurs prédictions, et ajuste dynamiquement leurs poids en fonction de leur précision relative au consensus.

---

#### **Fonctionnement :**
1. **Prédictions et Agrégation :**
   - Chaque modèle renvoie une prédiction et des probabilités associées à chaque classe.
   - Les probabilités des modèles sont multipliées par leurs poids respectifs avant d'être agrégées pour déterminer une **prédiction consensuelle**.

2. **Mise à jour des Poids :**
   - Les poids des modèles sont initialisés à `1.0`.
   - Après chaque prédiction, les poids sont ajustés :
     - **Bonus** (`+0.1`) : Si un modèle est d'accord avec le consensus.
     - **Malus** (`-0.1`) : Si un modèle est en désaccord avec le consensus.
   - Les poids sont contraints dans l'intervalle `[0.0, 1.0]`.

3. **Évaluation Globale :**
   - Le modèle agrégé est évalué sur un ensemble de test en calculant sa **précision globale**.

---

#### **Résultats :**

![image](https://github.com/user-attachments/assets/193d8eb1-cf04-4b27-a33c-669a156b2c2d)
---

#### **Interprétation :**
- Tous les modèles se sont avérés parfaitement alignés avec le consensus sur l'ensemble de test, d'où des poids finaux inchangés à `1.0`.
- Cela est cohérent avec la simplicité du dataset Iris, où tous les modèles atteignent déjà une précision de 100%.



#### **Conclusion :**
Le mécanisme de pondération garantit qu’à long terme, les modèles les plus fiables contribuent davantage au consensus, tout en pénalisant les modèles imprécis. Bien que ce mécanisme n'ait pas eu d'impact notable sur ce dataset (Iris), il est crucial dans des scénarios où les modèles ont des performances variables.


# **Question 4 : Proof-of-Stake avec Slashing**

### **Objectif**
Implémenter un mécanisme de **Proof-of-Stake avec slashing**, où :
1. Chaque modèle effectue un dépôt initial de 1000 euros pour participer au système.
2. Les modèles sont pénalisés (slashing) s'ils ne contribuent pas à des prédictions précises, réduisant leur solde et leur influence dans le système.
3. Les modèles performants gagnent en poids et conservent leur balance initiale.

---

### **Fonctionnement**
1. **Dépôt initial :** 
   - Chaque modèle commence avec un dépôt de 1000 euros, enregistré dans un fichier JSON local (`model_balances.json`).
   
2. **Mise à jour des poids et slashing :** 
   - Les modèles qui s'alignent avec la prédiction consensuelle gagnent un bonus de poids (`+0.1`).
   - Les modèles qui ne s'alignent pas subissent une pénalité financière de 50 euros.
   - Si un modèle atteint un solde de 0 euros, il est exclu du système.

3. **Précision globale :**
   - Le consensus des modèles est calculé via une agrégation pondérée des probabilités, en tenant compte des poids dynamiques.

---

### **Résultats**
![image](https://github.com/user-attachments/assets/9ef61e78-182f-4f59-8729-a2c8d4632c08)

---

### **Analyse des résultats**
1. **Précision parfaite :**
   - Tous les modèles ont contribué de manière cohérente aux prédictions consensuelles, expliquant pourquoi les poids finaux sont restés inchangés à `1.0`.

2. **Balances inchangées :**
   - Aucun modèle n'a été pénalisé car ils ont tous fourni des prédictions correctes, reflétant la simplicité du dataset Iris.

3. **Robustesse :**
   - Le mécanisme de slashing n'a pas été activé dans ce cas, mais il reste utile pour des datasets plus complexes où des modèles peuvent produire des prédictions incorrectes.

---

### **Étapes pour exécuter**
1. **Lancer les serveurs Flask :**
   - Exécute les fichiers `Code_1.py`, `Code_2.py`, `Code_3.py`, `Code_4.py` pour démarrer les serveurs Flask.

2. **Exécuter le script Proof-of-Stake :**
   ```bash
   python Proof_of_Stake_slashing.py
   ```

3. **Observer les résultats :**
   - La précision agrégée.
   - Les poids finaux des modèles.
   - Les balances finales sauvegardées dans `model_balances.json`.

---

### **Conclusion**
Le mécanisme de **Proof-of-Stake avec slashing** introduit un système de responsabilisation, où seuls les modèles performants et fiables maintiennent leur influence et leur dépôt. Bien que les résultats sur le dataset Iris montrent une performance parfaite (aucune pénalité appliquée), ce système est essentiel dans des environnements réels pour garantir l'intégrité et la fiabilité des prédictions.

---


terminal : pip install flask scikit-learn

http://127.0.0.1:5000/predict?sepal_length=5.1&sepal_width=3.5&petal_length=1.4&petal_width=0.2
