# EuroSAT land-use classification

A CNN trained from scratch on EuroSAT: 27,000 Sentinel-2 RGB image patches (64×64 px) in 10 land-use
classes (forest, river, highway, residential, industrial, crops and others).

**Approach**
- disjoint 80/20 train/validation split with a fixed seed
- augmentation inside the model (flips, rotation, zoom). Satellite images have no fixed "up", so all of these are valid
- 3 conv blocks with batch norm, global average pooling and dropout
- early stopping and learning-rate reduction on plateau
- per-class report and confusion matrix

**Results**

**92.9 % validation accuracy** on 5,400 held-out images (macro F1 0.93), up from 79 % in my first version.

| Best classes | F1 | Weakest classes | F1 |
|---|---|---|---|
| SeaLake | 0.99 | PermanentCrop | 0.88 |
| Forest | 0.98 | HerbaceousVegetation | 0.88 |
| Industrial | 0.94 | Highway | 0.90 |

The vegetation classes (permanent crop, herbaceous vegetation, pasture) are the hardest to tell apart from
above. Highway has the lowest recall (0.84), and Residential the lowest precision (0.86), so some other classes
get labelled residential. The validation set also picks the early-stopping epoch, so
the score is slightly optimistic. A separate test split would make it cleaner.

**What fixed training:** with Keras' default BatchNorm momentum (0.99), validation accuracy jumped between
~50 % and ~80 % from one epoch to the next, and early stopping cut the run off at 79 %. With momentum 0.9 it still
fluctuates (0.80–0.93) but trains for 25 epochs and settles above 90 %.

Transfer learning from a pretrained network is the obvious next step.

Put the course zip (`Group A -Eurosat Classification*.zip`) next to the notebook (on Colab: upload it to `/content`). A GPU helps but isn't required.

*University group project (Group A), M.Sc. Smart Energy Systems.*
