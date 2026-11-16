# Feature Agreement and Decision-Threshold Shift in Brain-Tumor MRI Classification Under Image Smoothing

This repository contains the Kaggle notebook (`statistical-image-analysis.ipynb`) used for the paper
"A Statistical Study of Feature Agreement and Decision-Threshold Shift in Brain-Tumor MRI
Classification Under Image Smoothing".

## Dataset

- Name: Brain Tumor (public dataset by Jakesh Bohaju)
- Link: https://www.kaggle.com/datasets/jakeshbohaju/brain-tumor
- Content: 3762 brain MRI slices (2079 non-tumor, 1683 tumor) and a CSV file with one row per image.
- The dataset is not included in this repository. Download it from the Kaggle link above, or
  attach it to a Kaggle notebook with "Add Input".

## What the notebook does

1. Checks the dataset (missing values, duplicate names, a constant feature that is removed).
2. Simulates small random changes to the supplied features and measures their reliability.
3. Recomputes 12 whole-image features from the images under six conditions: the original image,
   Gaussian smoothing (sigma 0.5, 1, 2) and median filtering (3x3, 5x5).
4. Measures how much each feature agrees across the six conditions (ICC(C,1) and ICC(A,1)),
   with bootstrap intervals.
5. Finds near-duplicate slices with a perceptual hash so that training and test images are kept apart.
6. Trains logistic regression and random forest models on original images and tests them on all
   six conditions (ROC-AUC, sensitivity, specificity).
7. Tests two repairs: training with filtered copies and recalibrating the threshold.
8. Tests which features cause the loss (stable features versus fragile features).

## What the notebook produces

Result tables (CSV files) and figures (PNG files), including:

- `image_processing_features.csv` and `extended_image_processing_features.csv`
  (recomputed features for every image and condition)
- `FINAL_feature_reliability.csv` (ICC values and change per filter strength)
- `FINAL_feature_family_test.csv` (stable versus fragile feature test)
- `paired_bootstrap_filter_changes.csv` and `validation_calibrated_test_results.csv`
- `logistic_regression_grouped_robustness.csv` and `random_forest_grouped_robustness.csv`
- Figures of feature distributions, ICC results and specificity versus filter strength

## How to run

1. Open the notebook on Kaggle and attach the dataset above as input.
2. Run the cells from top to bottom. The package `pingouin` is installed inside the notebook.
3. Environment used: Python 3.13, NumPy 2.5.4, pandas 2.3.3, scikit-learn 1.6.1, SciPy 1.16.3,
   scikit-image 0.25.2, Pillow 13.0.0, Matplotlib 3.11.2. Random seeds are fixed in the code.
