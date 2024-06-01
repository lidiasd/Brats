# Brats
# Projet de la segmentation semantiques des tumeurs cérébrales à partir d'images IRM (Imagerie par Résonance Magnétique) 

## Résumé
Ce projet se concentre sur la segmentation des tumeurs dans les images IRM cérébrales en utilisant le jeu de données BRATS 2021. La méthode proposée repose sur un modèle U-Net 2D, appliquant la fusion précoce pour intégrer les quatre modalités d'imagerie : T1, T1c, T2 et FLAIR.

Cette approche permet la détection et l'extraction automatiques des sous-régions tumorales, incluant la nécrose, l'œdème et la tumeur active. Nous avons évalué notre modèle sur les ensembles de données d'entraînement et de validation BRATS 2021, totalisant 1250 IRM cérébrales.

Les résultats de cette méthode sont prometteurs, avec des scores Dice de 69,19 % pour la tumeur nécrose, 72,72 pour la tumeur œdème et 80,01 % pour tumeur active sur 10 % de l'ensemble de données de validation. Cette approche offre une segmentation précise et rapide des gliomes, ouvrant la voie à des avancées significatives dans le diagnostic et le traitement des tumeurs cérébrales.

## Introduction

L'imagerie par résonance magnétique (IRM) est un outil crucial pour le diagnostic des tumeurs cérébrales. Cependant, la segmentation manuelle des tumeurs dans les images IRM est une tâche très complexe. D'où l'intérêt de l'automatisation de la segmentation des tumeurs cérébrales. Nous proposons donc une méthode basée sur un modèle U-Net 2D.

## Méthode

### Dataset && Paramètres
Le jeu de données BRATS 2021 contient des IRM multiparamétriques (mpMRI) de gliomes, avec des diagnostics pathologiques confirmés et des informations sur la méthylation du promoteur MGMT qui sont utilisées pour entraîner, valider et tester les modèles dans le défi BRATS de l’anée 2021. Les scans mpMRI comprennent différentes modalités telles que T1, T1-ce, T2 et T2-FLAIR, et ont été annotés manuellement par des experts pour identifier les sous-régions tumorales, telles que la tumeur améliorée par le Gadolinium, le tissu péri-tumoral envahi et le noyau tumoral nécrotique. Le jeu de données dans cette étude est composé de 1251 images : 1012 pour l'entraînement, 126 pour la validation, et 113 pour le test.
Pendant l'entraînement, nous utilisons un learning_rate   de 0.001 sur 15 époques, avec des images de taille 128x128. Les métriques évaluées comprennent MeanIoU (pour quatre classes), dice_coef, précision, sensibilité, spécificité, et à nouveau dice_coef pour assurer une évaluation globale complète.

## Modèle U-Net
U-Net est une architecture pour la segmentation sémantique. Il se compose d'un chemin de contraction et d'un chemin d'expansion. Le chemin de contraction suit l'architecture typique d'un réseau convolutionnel. Il consiste en l'application répétée de deux convolutions 3x3 (convolutions sans remplissage), chacune suivie d'une unité linéaire rectifiée (ReLU) et d'une opération de pooling max 2x2 avec stride 2 pour le sous-échantillonnage.

![Unet](images/unet.png) 

### Architecture de la méthode par fusion précoce des quatre modalités


![Architecture](images/unet2D_4mod.png)

### Résultats 

![Architecture_](images/curve_train_m1.png)

À l'époque 11 sur 15, les résultats sur l'ensemble de test montrent une performance globale moyenne du modèle. La métrique Mean IoU (Intersection over Union) est de 0.3931, indiquant une précision dans la délimitation des régions de tumeurs. Le dice coefficient, qui mesure la similarité entre les prédictions et les vérités terrain, est élevé à 61,23 %. Les valeurs de précision, sensibilité et spécificité sont également élevées, démontrant la capacité du modèle à bien classifier les différents types de tumeurs. En ce qui concerne les sous-régions tumorales, les coefficients de Dice pour la nécrose, l'œdème et la tumeur active sont respectivement de 0.5846, 0.6964 et 0.7215, avec des valeurs plus élevées pour l'œdème et la tumeur active, ce qui suggère une segmentation précise de ces régions.

Les résultats sur l'ensemble de validation montrent une performance moyenne du modèle. La métrique Mean IoU (Intersection over Union) est de 39,37 %, indiquant une précision moyenne dans la délimitation des régions de tumeurs. Le dice coefficient, mesurant la similarité entre les prédictions et les annotations, est également élevé à 63,95 %, soulignant une forte corrélation entre les deux. Les valeurs de précision, sensibilité et spécificité sont également élevées, démontrant la capacité du modèle à classifier avec précision les différentes classes de tumeurs. Pour les sous-régions tumorales, les coefficients de Dice pour la nécrose, l'œdème et la tumeur active sont respectivement de 61,00 %, 76,01 % et 76,92 %, confirmant une segmentation précise de ces régions.

Des examples

![""""""](images/example_m1.png)

 
### Architecture de la méthode par fusion précoce des quatre modalités moyenne

![Architecture](images/architecture_1.png)

### Résultats 

![Architecture_](images/curve_train_m2.png)
 
Les résultats sur l'ensemble de validation montrent une performance remarquable du modèle. La métrique Mean IoU (Intersection over Union) est élevée à 82,66 %, indiquant une précision significative dans la délimitation des régions de tumeurs. Le dice coefficient, qui mesure la similarité entre les prédictions et les annotations, est également satisfaisant à 52,95 %, soulignant une corrélation raisonnable entre les deux. Les valeurs de précision et de sensibilité sont élevées, respectivement à 99,13 % et 98,94 %, démontrant la capacité du modèle à classifier avec précision les différentes classes de tumeurs. La spécificité est également élevée, à 99,71 %, ce qui confirme la capacité du modèle à identifier les vrais négatifs. En ce qui concerne les sous-régions tumorales, les coefficients de Dice pour la nécrose, l'œdème et la tumeur active sont respectivement de 49,11 %, 56,95 % et 61,45 %, indiquant une segmentation partiellement précise de ces régions.

Les résultats sur l'ensemble de test montrent une performance moyenne également. La métrique Mean IoU (Intersection over Union) est élevée à 77,00 %, indiquant une précision moyenne dans la délimitation des régions de tumeurs. Le dice coefficient, qui mesure la similarité entre les prédictions et les annotations, est également satisfaisant à 53,71 %, soulignant une corrélation raisonnable entre les deux. Les valeurs de précision et de sensibilité sont élevées, respectivement à 99,05 % et 98,84 %, démontrant la capacité du modèle à classifier avec précision les différentes classes de tumeurs. La spécificité est également élevée, à 99,68 %, ce qui confirme la capacité du modèle à identifier les vrais négatifs. En ce qui concerne les sous-régions tumorales, les coefficients de Dice pour la nécrose, l'œdème et la tumeur active sont respectivement de 48,01 %, 57,67 % et 63,42 %, indiquant une segmentation raisonnablement précise de ces régions.

Des examples

![""""""](images/examples_m2.png)

example tranches 

![""""""](images/example_m2_1.png)

example tranches 

![""""""](images/example_m2_2.png)


### Architecture de la méthode par fusion précoce des 2 modalités 

![Architecture](images/unet2D_2mod.png)

### Résultats 

![Architecture_](images/curve_train_m3.png)
 
Les résultats sur l'ensemble de validation montrent une performance remarquable du modèle. La métrique Mean IoU (Intersection over Union) est élevée à 83,51 %, indiquant une précision significative dans la délimitation des régions de tumeurs. Le dice coefficient, qui mesure la similarité entre les prédictions et les annotations, est également satisfaisant à 64,82 %, soulignant une corrélation raisonnable entre les deux. Les valeurs de précision et de sensibilité sont élevées, respectivement à 99,42 % et 99,27 %, démontrant la capacité du modèle à classifier avec précision les différentes classes de tumeurs. La spécificité est également élevée, à 99,80 %, ce qui confirme la capacité du modèle à identifier les vrais négatifs. En ce qui concerne les sous-régions tumorales, les coefficients de Dice pour la nécrose, l'œdème et la tumeur active sont respectivement de 69,19 %, 72,72 % et 80,01 %, indiquant une segmentation raisonnablement précise de ces régions.
Les résultats sur l'ensemble de test montrent une performance remarquable du modèle. La métrique Mean IoU (Intersection over Union) est élevée à 0.8360, indiquant une précision significative dans la délimitation des régions de tumeurs. Le dice coefficient, qui mesure la similarité entre les prédictions et les annotations, est également satisfaisant à 63,25 %, soulignant une corrélation raisonnable entre les deux. Les valeurs de précision et de sensibilité sont élevées, respectivement à 99,35 % et 99,22 %, démontrant la capacité du modèle à classifier avec précision les différentes classes de tumeurs. La spécificité est également élevée, à 99,78 %, ce qui confirme la capacité du modèle à identifier les vrais négatifs. En ce qui concerne les sous-régions tumorales, les coefficients de Dice pour la nécrose, l'œdème et la tumeur active sont respectivement de 65,11 %, 71,50 % et 76,19 %, indiquant une segmentation raisonnablement précise de ces régions.

Des examples

![""""""](images/examples_m3.png)

example tranches 

![""""""](images/example1_m3.png)

example tranches 

![""""""](images/example2_m3.png)
## Installation

1. Cloner ce dépôt :

```bash
git clone https://github.com/votre-utilisateur/projet-reconnaissance-chiffres-manuscrits.git
```

2. Installer les dépendances :

```bash
pip install -r requirements.txt
```

3. Lancer le script principal :

```bash
python main.py
```

## Contributions

Les contributions sont les bienvenues ! Si vous souhaitez contribuer à ce projet, veuillez ouvrir une demande d'extraction avec vos modifications.

## Licence

Ce projet est sous licence MIT. Voir le fichier LICENSE pour plus de détails.

---

Pour toute question ou commentaire, veuillez contacter l'auteur du projet à [email@example.com](mailto:email@example.com).
