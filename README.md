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

_Results will be added after the next run. The classification report gives per-class precision/recall. (My first version reached 79 % validation accuracy, but its train/validation split could overlap. This version fixes that.)_

Most errors are between classes that look alike: highway vs. river, and permanent crop vs. pasture or
herbaceous vegetation. Transfer learning from a pretrained network is the obvious next step.

Put the dataset zip next to the notebook (on Colab: upload it to `/content`). A GPU helps but isn't required.

*University group project (Group A), M.Sc. Smart Energy Systems.*
