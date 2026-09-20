# Lightweight CNN for NEC Classification from Neonatal Abdominal X-rays

Reproducible PyTorch experiments for three-class classification of neonatal abdominal X-rays into **medical NEC (Mn), surgical NEC (Sn), and no pathology (Np)** using the GOSH NEC dataset.

[![Open in Google Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

## Overview

Necrotizing enterocolitis (NEC) is a serious gastrointestinal disease affecting neonates. This project investigates the use of a lightweight convolutional neural network (CNN) to classify neonatal abdominal X-rays into three diagnostic categories:

* **Mn** - Medical NEC
* **Sn** - Surgical NEC
* **Np** - No pathology

The project focuses on a reproducible evaluation of CNN depth and image augmentation strategies while keeping the model relatively lightweight.

## Dataset

This project uses the publicly available **GOSH NEC dataset** from the UCL Research Data Repository.

**The dataset and its images are not included in this repository.** Users must obtain the dataset separately from the official data repository and comply with its applicable access and licensing terms.

Dataset source:

* [GOSH NEC UCL Research Data Repository](https://rdr.ucl.ac.uk/articles/dataset/GOSH_NEC/26042824)

The notebook expects the user to provide their own authorized copy of the dataset.

## Method

The project uses a lightweight CNN implemented in **PyTorch** for three-class image classification.

The experimental workflow includes:

1. Dataset preparation and patient-level splitting
2. Grayscale image preprocessing and resizing
3. Reproducible training across multiple random seeds
4. CNN depth comparison
5. Geometric and intensity-based augmentation experiments
6. Gaussian pixel-intensity perturbation
7. Physics-informed photon-counting noise
8. Evaluation using multiple classification metrics
9. Final evaluation on a held-out test set

The test set is kept isolated from model and augmentation selection.

## CNN Depth Experiment

Different network depths were evaluated using repeated training runs.

| Convolutional Layers | Parameters | Validation Macro-F1 | Validation Macro-AUC |
| -------------------: | ---------: | ------------------: | -------------------: |
|                    1 |        123 |              0.2461 |               0.6003 |
|                    2 |        723 |              0.2375 |               0.5715 |
|                    4 |      4,299 |              0.4002 |               0.6033 |
|                    8 |     36,987 |              0.4281 |               0.6544 |
|                   16 |    111,483 |              0.4301 |               0.6874 |

The **16-convolution-layer configuration** was selected using validation Macro-F1, with Macro-AUC used as the tie-break criterion.

The reported values are means across reproducible runs; the notebook contains the corresponding standard deviations and additional evaluation metrics.

## Evaluation

Model performance is evaluated using:

* Macro-F1
* Accuracy
* Macro ROC-AUC
* Macro Average Precision
* Confusion matrices
* Class-wise performance

The final held-out test set is not used for selecting the CNN depth or augmentation configuration.

## Reproducing the Experiments

### 1. Obtain the dataset

Download the GOSH NEC dataset from the official UCL Research Data Repository and ensure that you have permission to use it under the applicable dataset terms.

### 2. Open the notebook

The main experiment is contained in:

`CHOC_NEC Classification_Code.ipynb`

The notebook can be opened directly in Google Colab from the GitHub repository.

### 3. Provide the dataset

The notebook requires the user to provide their own copy of the GOSH NEC dataset. Dataset files are not included in this repository.

### 4. Run the notebook

Run the notebook cells in order. Results and experiment outputs are saved to the user's own working/output directory.

Because the repository does not distribute the original dataset or private split artifacts, independently generated runs may use different patient-level splits and therefore may not produce identical numerical results to the reported experiments.

## Repository Structure

```text
nec-xray-lightweight-cnn/
│
├── README.md
└── CHOC_NEC Classification_Code.ipynb
```

## Important Data Note

This repository contains **code and research documentation only**.

The following are excluded:

* GOSH NEC images
* GOSH NEC dataset archives
* Patient metadata
* Private dataset split files
* Model checkpoints containing trained artifacts
* Internal CHOC materials or information

Please do not upload or redistribute the GOSH NEC dataset through this repository.

## Disclaimer

This project is a research and educational implementation. The models and results presented here are not intended for clinical diagnosis or clinical decision-making.

## Acknowledgment

This work uses the publicly available GOSH NEC dataset. Please refer to the official dataset record for the dataset's authorship, citation requirements, licensing, and terms of use.

## Citation

If you use this repository or build upon this work, please cite the associated project/report and the original GOSH NEC dataset according to the citation requirements provided by the dataset authors.
