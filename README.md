# Travail final 🧠🐍 

## Description du projet
Pour ce travail, j'ai choisi le projet _Unveiling Children's Theory of Mind with rs-fMRI_ créé par Wei-Hung Lin, & Syuan-Yu Lin et publié le 5 juin 2023. Ce projet visait à comprendre si la **connectivité fonctionnelle** peut être utilisée pour prédire la **théorie de l'esprit** (TdE) chez les **enfants**. Ce projet utilisait des **algorithmes d'apprentissage automatique supervisé** appliqués à des données d'IRMf afin de prédire les capacités de ToM chez les enfants.

Un jeu de données d'IRMf  au repos prétraité provenant du _Nilearn Development fMRI_ à été sélectionné pour réaliser ce projet. Ce jeu de données d'IRMf-repos est issu d'une étude portant sur le développement de régions cérébrales sociales fonctionnellement spécialisées, dans laquelle les participants regardaient un court métrage durant l'acquisition des données d'IRMf. Tous les enfants ont complété une tâche explicite du TdE conçue sur mesure afin de mesurer leurs capacités de TdE. 

### Données
122 enfants
* Âge moyen 6,71 ans (3–12 ans)
* Score TdE moyen = 0,775

### Préparation
Utilisation de l'atlas BASC à 64 parcelles pour extraire les séries temporelles

### Modèle
Validation croisée k-fold sur des données d'entraînement: 85 sujets
Évaluation des performances sur l’ensemble de test: 37 sujets
<img width="576" height="432" alt="image" src="https://github.com/user-attachments/assets/dba5afca-707e-4e71-b0dc-ac68f8d7c27b" />

### Interprétation
Matrice 64×64 pour identifier les connexions les plus prédictives du ToM
Visualisation via matrice et connectome cérébral
<img width="835" height="661" alt="image" src="https://github.com/user-attachments/assets/974efa5a-9365-41b2-97a8-93e69fa65abd" />

<img width="680" height="280" alt="image" src="https://github.com/user-attachments/assets/73727549-1a6a-4ade-97e0-1bc65095cb83" />


Les résultats des modèles d'apprentissage automatique ont révèlé des résultats cohérents en matière de connectivité fonctionnelle. Les auteures ont également observé the rôle primordial du cortex orbitopréfrontal. Cependant, les auteures mentionnnent que leur modèle nécessite encore des améliorations pour prédire les capacités de ToM des enfants à partir de leur connectivité fonctionnelle.

## Choix du projet
J'ai décidé de choisir ce projet puisque mon projet de maîtrise porte également sur l'association entre la théorie de l'esprit chez les enfants et la connectivité fonctionnelle au repos. Même si mon projet de maîtrise n'utilise pas d'algorithmes d'apprentissage automatique, les tâches et les connaissances que j'acquerrai pourront être transférables à mon propre projet.

## Tâches
Mes choix de tâches ont été influencées par les directions futures proposés ar les deux autrices. 
En effet les autrices proposaient:
* Utiliser un atlas bilatéral pour capturer l'association entre les deux hémisphères et les capacités de TdE
* Utiliser d'autres algorithmes d'apprentissage automatique pour confirmer nos résultats actuels
* Se concentrer sur les ROIs principales pour obtenir une compréhension plus approfondie de l'association entre la connectivité fonctionnelle et les capacités de ToM

### Tâche 1: Changement d'atlas
Dans le projet original l'atlas _BASC_ (Bootstrap Analysis of Stable Clusters) a été utilisé. 
+ : Ses parcelles sont définies par regroupement de voxels similaires
- : Les résulats peuvent être plus difficilement interprétable

Pour mon projet l'atlas _Yeo_ sera donc utlisé. Cet atlas est basé sur des réseaux fonctionnels (DMN, attentionel, frontopariétal, etc) 
+ : Systèmes cérébraux bien établis dans la littérature ce qui facilite l'interprétation des résultats en lien avec la ToM
+ : Yeo est plus répandu dans la littérature sur la cognition sociale
+ :  Yeo est directement accessible dans Nilearn
+ : Compatible avec NiftiLabelsMasker

<img width="747" height="401" alt="image" src="https://github.com/user-attachments/assets/a4b17e3c-ce6c-4d0b-b08a-d218ab8592e0" />

#### Étapes
1. Reproduire leur notebook
2. Importer le nouvel atlas Yeo depuis Nilearn
3. Reproduire le code original en y apportant les modifications nécessaires (correction de bogues, mise à jour du code désuet, etc.)
4. Répertorier et documenter les modifications effectuées

### Tâche 2: Création d'un connectogramme
Dans le projet des autrices des matrices et des connectomes ont été utilisé
+: Fourni beaucoup d'information
-: Peut devenir facilement incompréhensible/illisible

Ma deuxième tâche consitera à créer un connectogramme. En effet, l'utlisation de connectogramme a plusieurs points positifs.
+ : Représente les données de manière intuitive, et permet de voir les patterns de connectivité de façon beaucoup plus claire
+ : Révèle des relations difficiles à voir dans une matrice ou illisible sur un connectome
+ : Facilite la communication scientifique

#### Étapes
1. Extraire le signal de chaque région (tous les réseaux Yeo)
2. Créer une matrice de corrélation entre les 7 réseaux
3. Créer un connectogramme
4. Isoler les régions du DMN **seulement** (avec un masque sur le réseau 1 de Yeo)
5. Extraire le signal de ces régions
6. Créer une matrice de corrélation des régions du DMN **seulement**
7. Créer un deuxième connectogramme

<img width="540" height="532" alt="image" src="https://github.com/user-attachments/assets/173b0067-c005-4b62-aa9d-ec5c695a4710" />

#### Si la tâche ne prend pas assez de temps
* Ajouter des seuils significatifs pour améliorer la visualisation
* Créer d'autres types de graphiques

### Tâche 3: Comparaison de modèles de prédiction
Ma trosième tâche consistera à comparer des modèles de prédiction. Dans l'étude originale, le modèle de prédiction avait été construit avec l'ensemble du cerveau. Mon objectif en effectuant cette comparaison est de déterminer s'il est vraiment nécessaire d'utiliser tout le cerveau ou si l'utilisation de régions clés est suffisante pour prédire la théorie de l'esprit.

#### Étapes:
1. Entraîner le modèle avec KFold avec les 7 réseaux
2. Évaluer la performance
3. Entraîner le modèle avec KFold avec le DMN **seulement**
4. Évaluer la performance
5. Comparer les différentes métriques (coefficient de détermination, l'erreur moyenne de prédiction, etc.)

#### Si la tâche ne prend pas assez de temps
* Retester avec d'autre modèle de prédiction que nous apprendrons.

## Source
Lin, S.-Y., & Lin, W.-H. (2023, June 23). Unveiling children's theory of mind with rs-fMRI [GitHub repository]. GitHub. https://github.com/WeiHungLin/Unveiling_children_ToM_with_rsfmri 

# FIN 🎉
