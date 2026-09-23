# Bridge Concrete Damage Detection Using Deep Learning

Deep learning project for detecting and classifying concrete bridge damage using **Xception** and a **Vanilla CNN optimized with Keras Tuner** on the CODEBRIM dataset.

## Overview

Concrete bridge inspections can involve multiple types of visible defects. This project performs **multi-label classification**, where one image can contain more than one damage class.

The project compares two approaches:

1. **Xception** with ImageNet transfer learning
2. **Vanilla CNN** with hyperparameter optimization using **Keras Tuner Hyperband**

## Damage Classes

The model predicts five damage classes:

- Crack
- CorrosionStain
- Efflorescence
- ExposedBars
- Spallation

## Dataset

This project uses the **CODEBRIM (COncrete DEfect BRidge IMage Dataset)**.

Official dataset:
https://zenodo.org/records/2620293

The notebook expects the dataset to be available locally with the following structure:

```text
dataset/
└── building/
    ├── train/
    │   ├── Images/
    │   └── Labels/
    ├── valid/
    │   ├── Images/
    │   └── Labels/
    └── test/
        ├── Images/
        └── Labels/
```

The raw dataset is not included in this repository because of its large size. Please download it from the official source above and place it in the expected directory structure.

## Dataset Split

The dataset used in the notebook contains:

| Split | Images |
|---|---:|
| Train | 3,899 |
| Validation | 1,141 |
| Test | 598 |

Images are resized to **299 × 299** pixels for the Xception model.

## Methodology

### 1. Data Preprocessing

- Load image-label pairs from the dataset directories
- Convert the five damage classes into multi-hot labels
- Resize images to 299 × 299
- Create TensorFlow datasets for training, validation, and testing

### 2. Xception

The Xception model uses ImageNet pretrained weights as the feature extractor.

The base model is initially frozen, followed by:

- Global Average Pooling
- Dense layer with 512 units and ReLU activation
- Output layer with 5 units and sigmoid activation

### 3. Vanilla CNN + Keras Tuner

A Vanilla CNN is optimized using **Keras Tuner Hyperband**.

The tuner searches for suitable CNN hyperparameters using validation binary accuracy as the optimization objective.

### 4. Threshold Optimization

Because this is a multi-label classification problem, the default threshold of 0.5 is also evaluated.

The project additionally searches thresholds from 0.1 to 0.9 for each class to improve the F1-score.

## Results

### Xception — Test Set

At the default threshold of 0.5:

| Metric | Score |
|---|---:|
| AUC | 0.9304 |
| Binary Accuracy | 0.8859 |
| Loss | 0.2613 |
| Top-K Accuracy | 0.9857 |
| Micro F1 | 0.80 |
| Macro F1 | 0.78 |

After class-specific threshold optimization:

| Metric | Score |
|---|---:|
| Micro F1 | 0.81 |
| Macro F1 | 0.80 |

### Vanilla CNN — Test Set

At the default threshold of 0.5:

| Metric | Score |
|---|---:|
| AUC | 0.9208 |
| Binary Accuracy | 0.8826 |
| Loss | 0.2900 |
| Top-K Accuracy | 0.9806 |
| Micro F1 | 0.77 |
| Macro F1 | 0.76 |

After class-specific threshold optimization:

| Metric | Score |
|---|---:|
| Micro F1 | 0.79 |
| Macro F1 | 0.78 |

## Evaluation

The models are evaluated using:

- Precision
- Recall
- F1-score
- Micro F1
- Macro F1
- AUC
- Binary Accuracy
- Top-K Accuracy
- Precision-Recall curves
- ROC curves
- Multi-label confusion matrices

## Repository Structure

```text
Bridge-concrete-damage-detection-using-deep-learning/
│
├── Bridge_concrete_damage_detection.ipynb
├── README.md
├── requirements.txt
├── .gitignore
│
└── dataset/
    └── README.md
```

## Installation

Create and activate a Python virtual environment, then install the dependencies:

```bash
pip install -r requirements.txt
```

The notebook was executed with **TensorFlow 2.19.1**.

## Running the Project

1. Download the CODEBRIM dataset from the official source.
2. Extract and place the required dataset under:

```text
dataset/building/
```

3. Install the dependencies:

```bash
pip install -r requirements.txt
```

4. Open:

```text
Bridge_concrete_damage_detection.ipynb
```

5. Run the notebook from the beginning.

## Notes

- GPU acceleration is recommended for model training.
- The dataset itself is not included in this repository.
- The notebook uses relative dataset paths so the project can be reproduced on another machine without changing absolute Windows/Linux paths.

## Reference

Mundt, M., Majumder, S., Murali, S., Panetsos, P., & Ramesh, V. (2019).
*Meta-learning Convolutional Neural Architectures for Multi-target Concrete Defect Classification with the COncrete DEfect BRidge IMage Dataset.*
IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR).

Dataset:
https://zenodo.org/records/2620293
