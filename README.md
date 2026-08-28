# OCTRetinaAI-Patch-Based-Retinal-Disease-Classification

# Overview

This project implements and experimentally extends the PatchBridgeNet research methodology for retinal disease classification using Optical Coherence Tomography (OCT) images from the OCTDL dataset.

The implementation combines patch-based deep feature extraction, pretrained CNN backbones, feature selection, classical machine learning, and hyperparameter optimization for both 7-class and binary retinal disease classification.

The reference PatchBridgeNet methodology uses MobileNetV2, DarkNet53, DenseNet201, INCA, Chi-Square feature selection, and SVM classification.

# Project Highlights
Implemented a patch-based OCT image classification pipeline.
Used 4 vertical patches along with the original image representation.
Extracted deep features using:
MobileNetV2
DarkNet53
DenseNet201
Applied INCA (Iterative NCA) for feature selection.
Applied Chi-Square (SelectKBest) for second-stage feature selection.
Used a polynomial-kernel SVM for classification.
Applied Optuna for hyperparameter optimization.
Tuned class-weight power to address the imbalanced OCTDL dataset.
# Evaluated both:
7-class retinal disease classification
Binary diseased vs normal classification
Evaluated performance using 10-fold Stratified Cross Validation.
Compared different patch counts, CNN backbones, feature-selection methods, and classical ML classifiers.

# Dataset

The project uses the OCTDL dataset, containing 2,064 OCT images across seven classes:

Class	                Images
AMD	                  1,231
NO (Normal)	            332
ERM	                    155
DME	                    147
RVO	                    101
VID	                    76
RAO	                    22
Total	                2,064

The dataset is imbalanced, with RAO being the smallest class.

The reference paper also describes OCTDL as an imbalanced dataset and evaluates both seven-class and binary classification tasks.

Note: The dataset itself is not included in this repository. Please download it separately and place it under the data/ directory.

# Methodology
```
                    OCT Image
                        │
                        ▼
              Resize to 224 × 224
                        │
                        ▼
            Original Image + 4 Patches
                        │
          ┌─────────────┼─────────────┐
          ▼             ▼             ▼
     MobileNetV2     DarkNet53     DenseNet201
          │             │             │
          └─────────────┼─────────────┘
                        ▼
              Deep Feature Extraction
                        │
                        ▼
                       INCA
                        │
                        ▼
                 Feature Fusion
                        │
                        ▼
                 Chi-Square Selection
                        │
                        ▼
                Optuna-Tuned SVM
                        │
              ┌─────────┴─────────┐
              ▼                   ▼
        7-Class Task        Binary Task

```

Class-wise Results
Class	Sensitivity	Specificity	Precision	F1-Score
AMD	97.40%	93.28%	95.54%	96.46%
DME	79.59%	98.80%	83.57%	81.53%
ERM	86.45%	99.27%	90.54%	88.45%
NO	94.28%	97.92%	89.68%	91.92%
RAO	81.82%	100.00%	100.00%	90.00%
RVO	70.30%	99.18%	81.61%	75.53%
VID	82.89%	99.80%	94.03%	88.11%
