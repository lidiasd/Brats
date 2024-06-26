# Projet de la segmentation semantiques des tumeurs cérébrales à partir d'images IRM (Imagerie par Résonance Magnétique) 

## Résumé
Ce projet se concentre sur la segmentation des tumeurs dans les images IRM cérébrales en utilisant le jeu de données BRATS 2021. La méthode proposée repose sur un modèle U-Net 2D, appliquant la fusion précoce pour intégrer les quatre modalités d'imagerie : T1, T1ce, T2 et FLAIR.

Cette approche permet la détection et l'extraction automatiques des sous-régions tumorales, incluant la nécrose, l'œdème et la tumeur active. J'ai évalué le modèle sur les ensembles de données d'entraînement et de validation et de test de BRATS 2021, totalisant 1250 IRM cérébrales.

Le modèle est correct, surpassant la moyenne, avec des scores Dice de 69,19 % pour la tumeur nécrose, 72,72 % pour la tumeur œdème et 80,01 % pour tumeur active sur 10 % de l'ensemble de données de validation. Cette approche offre une segmentation précise et rapide des gliomes, ouvrant la voie à des avancées significatives dans le diagnostic et le traitement des tumeurs cérébrales.

## Introduction

L'imagerie par résonance magnétique (IRM) est un outil crucial pour le diagnostic des tumeurs cérébrales. Cependant, la segmentation manuelle des tumeurs dans les images IRM est une tâche très complexe. D'où l'intérêt de l'automatisation de la segmentation des tumeurs cérébrales. Je propose donc une méthode basée sur un modèle U-Net 2D qui permet de relever ce défi.

## Modèle U-Net
U-Net est une architecture pour la segmentation sémantique. Il se compose d'un chemin de contraction et d'un chemin d'expansion. Le chemin de contraction suit l'architecture typique d'un réseau convolutionnel. Il consiste en l'application répétée de deux convolutions 3x3 (convolutions sans remplissage), chacune suivie d'une unité linéaire rectifiée (ReLU) et d'une opération de pooling max 2x2 avec stride 2 pour le sous-échantillonnage.

![Unet](images/unet.png) 

## Méthode

### Dataset && Paramètres
Le jeu de données BRATS 2021 contient des IRM multiparamétriques (mpMRI) de gliomes, avec des diagnostics pathologiques confirmés et des informations sur la méthylation du promoteur MGMT qui sont utilisées pour entraîner, valider et tester les modèles dans le défi BRATS de l’anée 2021. Les scans mpMRI comprennent différentes modalités telles que T1, T1-ce, T2 et T2-FLAIR, et ont été annotés manuellement par des experts pour identifier les sous-régions tumorales, telles que la tumeur améliorée par le Gadolinium, le tissu péri-tumoral envahi et le noyau tumoral nécrotique. Le jeu de données dans cette étude est composé de 1251 images : 1012 pour l'entraînement, 126 pour la validation, et 113 pour le test.
Pendant l'entraînement, j'utilise un learning rate   de 0.001 sur 15 époques, avec des images de taille 128x128 et un batch size de 2. Les métriques évaluées comprennent MeanIoU (pour quatre classes) car elle permet d'évaluer globalement la méthode, dice_coef, précision, sensibilité, spécificité pour assurer une évaluation complète.

### Architecture de la méthode par fusion précoce des quatre modalités

Cette méthode se distingue par la fusion précoce des quatre modalités d'imagerie IRM (T1, T1ce, T2 et Flair). En combinant ces différentes modalités dès les premières couches du réseau, comme illustré ci-dessous, j'exploite de manière optimale les informations des quatres modalités en même temps.

![Architecture](images/unet2D_4mod.png)

### Résultats 

![Architecture_](images/curve_train_m1.png)

À l'époque 11 sur 15, les résultats sur l'ensemble de test montrent une performance globale modérée du modèle. La métrique Mean IoU (Intersection over Union) est de 39,31 %. Le Dice coefficient, qui mesure la similarité entre les prédictions et les vérités terrain, est de 61,23 %. Les valeurs de précision, sensibilité et spécificité sont élevées, démontrant la capacité du modèle à classifier les différents types de tumeurs. En ce qui concerne les sous-régions tumorales, les coefficients de Dice pour la nécrose, l'œdème et la tumeur active sont respectivement de 58,46 %, 69,64 % et 72,15 %, avec des valeurs plus élevées pour l'œdème et la tumeur active, ce qui suggère une segmentation moyenne de ces régions.

Les résultats sur l'ensemble de validation montrent une performance modérée du modèle. La métrique Mean IoU (Intersection over Union) est de 39,37 %. Le Dice coefficient, mesurant la similarité entre les prédictions et les verités terains, est de 63,95 %, soulignant une corrélation entre les deux. Les valeurs de précision, sensibilité et spécificité sont également élevées. Pour les sous-régions tumorales, les coefficients de Dice pour la nécrose, l'œdème et la tumeur active sont respectivement de 61,00 %, 76,01 % et 76,92 %, montrant une segmentation moyenne de ces régions, mais globalement, le modèle reste inférieur à la moyenne.

Des examples 

![""""""](images/example_m1.png)

 
### Architecture de la méthode par fusion précoce des quatre modalités moyenne

Cette méthode se distingue par la fusion précoce des quatre modalités d'imagerie IRM (T1, T1ce, T2 et Flair). En combinant ces différentes modalités dès les premières couches du réseau, comme illustré ci-dessous, j'exploite de manière optimale les informations des quatre modalités en même temps, mais cette fois en calculant la moyenne des quatre modalités.

![Architecture](images/architecture_1.png)

### Résultats 

![Architecture_](images/curve_train_m2.png)
 
Les résultats sur l'ensemble de validation montrent une performance remarquable du modèle. La métrique Mean IoU (Intersection over Union) est élevée à 82,66 %, indiquant une précision significative dans la délimitation des régions de tumeurs. Le dice coefficient, qui mesure la similarité entre les prédictions et les vérités terrains, est également satisfaisant à 52,95 %, soulignant une corrélation raisonnable entre les deux. Les valeurs de précision et de sensibilité sont élevées, respectivement à 99,13 % et 98,94 %, démontrant la capacité du modèle à classifier avec précision les différentes classes de tumeurs. La spécificité est également élevée, à 99,71 %, ce qui confirme la capacité du modèle à identifier les vrais négatifs. En ce qui concerne les sous-régions tumorales, les coefficients de Dice pour la nécrose, l'œdème et la tumeur active sont respectivement de 49,11 %, 56,95 % et 61,45 %, indiquant une segmentation partiellement précise de ces régions.

Les résultats sur l'ensemble de test montrent une performance remarquable également. La métrique Mean IoU (Intersection over Union) est élevée à 77,00 %, indiquant une précision élevée dans la délimitation des régions de tumeurs. Le dice coefficient, qui mesure la similarité entre les prédictions et les vérités terrains, est également satisfaisant à 53,71 %, soulignant une corrélation raisonnable entre les deux. Les valeurs de précision et de sensibilité sont élevées, respectivement à 99,05 % et 98,84 %, démontrant la capacité du modèle à classifier avec précision les différentes classes de tumeurs. La spécificité est également élevée, à 99,68 %, ce qui confirme la capacité du modèle à identifier les vrais négatifs. En ce qui concerne les sous-régions tumorales, les coefficients de Dice pour la nécrose, l'œdème et la tumeur active sont respectivement de 48,01 %, 57,67 % et 63,42 %, indiquant une segmentation raisonnablement précise de ces régions.

Des examples

![""""""](images/examples_m2.png)

Des examples detaillés 

![""""""](images/example_m2_1.png)

Des examples detaillés 

![""""""](images/example_m2_2.png)


### Architecture de la méthode par fusion précoce des 2 modalités (T1ce et Flair)

Cette méthode se distingue par la fusion précoce des deux modalités d'imagerie IRM (T1ce et Flair). En combinant ces deux modalités dès les premières couches du réseau, comme illustré ci-dessous, j'exploite de manière optimale les informations des deux modalités en même temps. Cette approche est inspirée des travaux ultérieurs.

![Architecture](images/unet2D_2mod.png)

### Résultats 

![Architecture_](images/curve_train_m3.png)
 
Les résultats sur l'ensemble de validation montrent une performance remarquable du modèle. La métrique Mean IoU (Intersection over Union) est élevée à 83,51 %, indiquant une précision significative dans la délimitation des régions de tumeurs. Le dice coefficient, qui mesure la similarité entre les prédictions et les vérités terrains, est également satisfaisant à 64,82 %, soulignant une corrélation raisonnable entre les deux. Les valeurs de précision et de sensibilité sont élevées, respectivement à 99,42 % et 99,27 %, démontrant la capacité du modèle à classifier avec précision les différentes classes de tumeurs. La spécificité est également élevée, à 99,80 %, ce qui confirme la capacité du modèle à identifier les vrais négatifs. En ce qui concerne les sous-régions tumorales, les coefficients de Dice pour la nécrose, l'œdème et la tumeur active sont respectivement de 69,19 %, 72,72 % et 80,01 %, indiquant une segmentation raisonnablement précise de ces régions.

Les résultats sur l'ensemble de test montrent une performance remarquable du modèle. La métrique Mean IoU (Intersection over Union) est élevée à 83,60 %, indiquant une précision significative dans la délimitation des régions de tumeurs. Le dice coefficient, qui mesure la similarité entre les prédictions et les vérités terrains, est également satisfaisant à 63,25 %, soulignant une corrélation raisonnable entre les deux. Les valeurs de précision et de sensibilité sont élevées, respectivement à 99,35 % et 99,22 %, démontrant la capacité du modèle à classifier avec précision les différentes classes de tumeurs. La spécificité est également élevée, à 99,78 %, ce qui confirme la capacité du modèle à identifier les vrais négatifs. En ce qui concerne les sous-régions tumorales, les coefficients de Dice pour la nécrose, l'œdème et la tumeur active sont respectivement de 65,11 %, 71,50 % et 76,19 %, indiquant une segmentation raisonnablement précise de ces régions.

Des examples

![""""""](images/examples_m3.png)

Des examples detaillés 

![""""""](images/example1_m3.png)

Des examples detaillés 

![""""""](images/example2_m3.png)

## Discussion
Lors des tests avec les modalités T1, T2 et leurs combinaisons avec T1ce et Flair, les résultats n'étaient pas satisfaisants, d'où le choix des deux modalités T1ce et Flair. D'après le tableau ci-dessous qui résume les résultats des trois modèles sur l'ensemble de validation, on déduit que, globalement, la méthode par fusion précoce des deux modalités (T1ce et FLAIR) est la plus performante. En effet, elle a atteint une valeur maximale de la moyenne d'IoU, ce qui évalue les performances globales du modèle.

![""""""](images/discussion.png)

Liens utiles : 

[Le code source ](https://drive.google.com/file/d/1_ZwxeaKktEOiTZtgeOHHpDAQEFzvrOfx/view?usp=sharing)
 
