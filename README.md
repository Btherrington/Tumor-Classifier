# Brain Tumor Gene Expression Classifier

A PyTorch neural network that classifies brain tumor types from TCGA gene expression data.

## Overview
Phase 1A of a multimodal project. Uses gene expression (RNA-seq) data from the TCGA GBM and LGG cohorts to classify samples into one of six tumor types:
- Glioblastoma
- Astrocytoma, NOS
- Astrocytoma, anaplastic
- Oligodendroglioma, NOS
- Oligodendroglioma, anaplastic
- Mixed glioma

Phase 1B will add an MRI image classifier for multimodal comparison.

## Dataset
TCGA gene expression and clinical phenotype data from UCSC Xena:
- [TCGA-GBM](https://xenabrowser.net/datapages/?cohort=GDC%20TCGA%20Glioblastoma%20(GBM))
- [TCGA-LGG](https://xenabrowser.net/datapages/?cohort=GDC%20TCGA%20Lower%20Grade%20Glioma%20(LGG))

Download both `STAR - FPKM` (gene expression) and `Phenotype` files for each cohort and place in a `data/` folder.

## Pipeline
1. Load and merge GBM + LGG expression matrices (60,660 genes × 709 samples)
2. Match samples to diagnosis labels, drop NaNs
3. 70/30 train/test split with shuffled indices
4. Feature selection with SelectKBest (ANOVA F-test) → top 2,000 genes
5. Train feedforward network (2,000 → 128 → 6) with ReLU and dropout
6. Evaluate on held-out test set

## Results
Test accuracy: ~58%

Limited by sample size (497 training samples across 6 classes) and biological noise. Future improvements: cross-validation, class balancing, feature engineering.

## Stack
Python, pandas, scikit-learn, PyTorch
