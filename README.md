# 🛰️ Satellite Land Cover Segmentation (DeepGlobe)

Segmentation sémantique d'images satellites avec le Deep Learning : comparaison de **trois architectures** (U-Net from scratch, VGG-UNet en transfer learning, DeepLabV3+ avec ResNet50) sur le dataset **DeepGlobe Land Cover Classification**, avec un focus sur la détection des **zones agricoles**.

---

## 🎯 Objectifs

1. Préparer les données et réaliser une analyse exploratoire (EDA) du dataset DeepGlobe.
2. Entraîner et évaluer trois modèles de segmentation sémantique.
3. Comparer leurs performances (Dice, IoU, convergence, temps d'entraînement).
4. Analyser en détail la classe **Agriculture** (confusions, taille des parcelles, visualisations).

## 🗂️ Dataset

**DeepGlobe Land Cover Classification Challenge** : images satellites haute résolution annotées en **6 classes** :

| Classe | Description |
|---|---|
| `urban` | Zones urbaines |
| `agriculture` | Zones agricoles |
| `rangeland` | Pâturages / prairies |
| `forest` | Forêts |
| `water` | Eau |
| `barren` | Sols nus |

Source : [DeepGlobe Land Cover Classification (Kaggle)](https://www.kaggle.com/datasets/balraj98/deepglobe-land-cover-classification-dataset)

## 📓 Contenu du dépôt

```
.
├── README.md
├── docs/
│   ├── methodology.md
│   
├── notebooks/
│   ├── 01_data_preparation_eda.ipynb
│   ├── 02_unet_from_scratch.ipynb
│   ├── 03_vgg_unet_transfer_learning.ipynb
│   ├── 04_deeplabv3plus_resnet50.ipynb
│   ├── 05_models_comparison.ipynb
│   └── 06_agriculture_focus_analysis.ipynb
└── requirements.txt
```

| # | Notebook | Description |
|---|---|---|
| 01 | `01_data_preparation_eda` | Imports, configuration, reproductibilité, exploration du dataset, statistiques des images, split train/validation |
| 02 | `02_unet_from_scratch` | U-Net entraîné de zéro, métriques personnalisées (Dice, IoU, Weighted Dice Loss), class weights |
| 03 | `03_vgg_unet_transfer_learning` | VGG-UNet avec encodeur VGG pré-entraîné (ImageNet), data augmentation |
| 04 | `04_deeplabv3plus_resnet50` | DeepLabV3+ : encodeur ResNet50, ASPP étendu à 5 branches, decoder optimisé, fine-tuning complet |
| 05 | `05_models_comparison` | Comparaison des 3 modèles : performances, convergence, heatmap par classe, radar chart |
| 06 | `06_agriculture_focus_analysis` | Focus agriculture : confusions, analyse par taille de parcelle, comparaisons visuelles |

## 🧠 Modèles comparés

- **U-Net (from scratch)** : architecture encodeur-décodeur avec skip connections, sans pré-entraînement.
- **VGG-UNet (transfer learning)** : U-Net dont l'encodeur est un VGG pré-entraîné sur ImageNet.
- **DeepLabV3+** : encodeur ResNet50 pré-entraîné, module ASPP (convolutions atrous) et decoder de type U-Net.

## 📊 Métriques

- **Dice coefficient** (métrique principale)
- **IoU** (Intersection over Union)
- **Weighted Dice Loss** (fonction de perte, gestion du déséquilibre de classes)

Les résultats détaillés sont dans les notebooks 05 et 06. Vous pouvez aussi résumer les scores finaux ici :

| Modèle | Dice (val) | IoU (val) | Dice Agriculture |
|---|---|---|---|
| U-Net from scratch | 0.816 | 0.692 | 0.886 |
| VGG-UNet | 0.858 | 0.755 | 0.913 |
| DeepLabV3+ | 0.863 | 0.763 | 0.920 |

## ⚙️ Environnement et technologies

- Python 3, TensorFlow / Keras
- NumPy, Pandas, SciPy, scikit-learn
- Matplotlib, Seaborn, Plotly
- Entraînement effectué sur **Kaggle** (GPU), mixed precision activée

Installation (pour ré-exécuter les notebooks originaux `.ipynb`) :

```bash
pip install -r requirements.txt
```

## 🔁 Reproductibilité

Les seeds (Python, NumPy, TensorFlow) sont fixés dans chaque notebook. Les résultats peuvent varier légèrement selon le matériel (GPU) utilisé.

## 🚀 Pistes d'amélioration

- Tester d'autres encodeurs (EfficientNet, ConvNeXt) ou des modèles à base de Transformers (SegFormer).
- Augmentations plus riches et entraînement sur des images plus grandes.
- Post-traitement des masques (nettoyage morphologique).

## 📄 Licence

Projet à but pédagogique. Le dataset DeepGlobe est soumis à sa propre licence : voir la page Kaggle.

## 👤 Auteur

**Chaimaa El Affas** — [GitHub](https://github.com/chaimaaelaffas1) · [chaimaa.elaffas1@gmail.com](mailto:chaimaa.elaffas1@gmail.com)
