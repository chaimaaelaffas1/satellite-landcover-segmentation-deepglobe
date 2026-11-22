# Méthodologie

## 1. Préparation des données (Notebook 01)

- Chargement des images satellites DeepGlobe et des masques associés.
- Analyse des dimensions, des statistiques RGB (valeurs 0-255 et normalisées [0, 1]).
- Étude de la distribution des classes (déséquilibre) et calcul des **class weights**.
- Split train / validation avec `train_test_split`.
- Fixation des seeds pour garantir la reproductibilité.

## 2. Entraînement des modèles (Notebooks 02 à 04)

| Élément | U-Net | VGG-UNet | DeepLabV3+ |
|---|---|---|---|
| Encodeur | Entraîné de zéro | VGG (ImageNet) | ResNet50 (ImageNet) |
| Transfer learning | Non | Oui | Oui (fine-tuning complet) |
| Data augmentation | — | Oui | Oui (renforcée x3) |
| Particularité | Skip connections | Skip connections + features pré-entraînées | ASPP 5 branches + decoder optimisé |

Éléments communs :

- Encodage **one-hot** des masques (6 classes).
- Fonction de perte : **Weighted Dice Loss**.
- Métriques : **Dice** et **IoU**.
- Callbacks Keras (early stopping, réduction du learning rate, sauvegarde du meilleur modèle).
- Optimiseur : Adam.

## 3. Évaluation comparative (Notebook 05)

- Tableau de synthèse des performances sur la validation.
- Courbes de convergence (Dice validation par epoch).
- Heatmap Dice par modèle et par classe.
- Radar chart multi-critères.

## 4. Focus agriculture (Notebook 06)

- Scores des 3 modèles sur la classe `agriculture`.
- Matrices de confusion et analyse des erreurs.
- Performance selon la taille des parcelles agricoles.
- Comparaisons visuelles sur des images satellites.

## 5. Définitions

- **Dice** = 2·|A∩B| / (|A| + |B|)
- **IoU** = |A∩B| / |A∪B|
- **ASPP** : Atrous Spatial Pyramid Pooling, convolutions dilatées à plusieurs taux pour capter le contexte multi-échelle.
