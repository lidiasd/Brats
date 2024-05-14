# Brats
# Projet de la segmentation semantiques des tumeurs cérébrales à partir d'images IRM (Imagerie par Résonance Magnétique)

## Résumé

Ce projet vise à résoudre le défi complexe de la segmentation des formes de tumeurs dans les images IRM du cerveau en utilisant le jeu de données BRATS 2021. La méthode propose une approche de segmentation basée sur un modèle U-Net 3D avec une fusion précoce des quatre modalités d'imagerie : T1, T1c, T2 et FLAIR.

Cette approche permet la détection et l'extraction automatiques des sous-régions des formes de tumeurs, comprenant la classe nécrose, l'œdème et la tumeur active. Nous avons évalué notre modèle sur les ensembles de données d'entraînement et de validation BRATS 2021, comprenant un total de 1250 IRM cérébrales.

Les résultats de cette méthode sont prometteurs, avec des scores Dice de ******** pour la tumeur en croissance (ET), **** pour la tumeur complète (WT) et **** pour le noyau tumoral (TC) sur 20 % de l'ensemble de données d'entraînement. Cette approche offre une segmentation précise et rapide des gliomes, ouvrant la voie à des avancées significatives dans le diagnostic et le traitement des tumeurs cérébrales.

## Introduction



## Méthode

### Collecte de données
Le jeu de données BRATS 2021 contient des IRM multiparamétriques (mpMRI) de gliomes, avec des diagnostics pathologiques confirmés et des informations sur la méthylation du promoteur MGMT. Ces données sont utilisées pour entraîner, valider et tester les modèles dans le défi BRATS de l’anée 2021. Les scans mpMRI comprennent différentes modalités telles que T1, T1-ce, T2 et T2-FLAIR, et ont été annotés manuellement par des experts pour identifier les sous-régions tumorales, telles que la tumeur améliorée par le Gadolinium, le tissu péri-tumoral envahi et le noyau tumoral nécrotique. Les fichiers DICOM associés seront publiés après le défi, et une correspondance entre les données BRATS et d'autres collections facilitera la recherche.


### Prétraitement des données
Les images sont normalisées et redimensionnées pour être adaptées à l'entrée du modèle CNN.
![Architecture_](images/data_distrb.png) 

## Modèle Unet 2D
description.
### Architecture de la méthode par fusion précoce des quatre modalités

![Architecture](images/unet2D_4mod.png)
### Résultats 
![Architecture_](images/first_model_curve_train.png)
### Architecture de la méthode par fusion précoce des deux modalités "Flair", "T1_ce"

![Architecture_](images/unet2D_2mod.png) 

### Résultats 

## Modèle Unet 2D

### Architecture de la méthode par fusion précoce des quatre modalités

### Résultats 
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
