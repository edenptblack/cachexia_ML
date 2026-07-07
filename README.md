# Cachexia metabolomics classifier

Binary classification of cancer-associated muscle wasting (cachexia) from urinary metabolite profiles. Five models are benchmarked with stratified cross-validation and the best is automatically selected by mean ROC-AUC, then evaluated on a held-out test set. The selected model (a support vector machine) achieved an AUC of 0.75 on the held-out test set with high sensitivity but low specificity. These results are reasonable but not clinically deployable, limited by the small sample size for training data (n = 23). Adapted from coursework for MSc Bioinformatics at Teesside University.

## Description

After cleaning and a log10 transform (with a +1 pseudocount), the data is explored with per-metabolite boxplots, a correlation heatmap, and PCA. Five classifiers (Logistic Regression, SVM, KNN, Random Forest, and Gradient Boosting) are each wrapped in a scikit-learn Pipeline (median
imputation + standard scaling) and compared under stratified 5-fold cross-validation on a 70/30 train/test split. The best model (highest mean ROC-AUC, lowest standard deviation as a tiebreaker) is selected automatically then refit and evaluated on the held-out set via a classification report, ROC curve, and AUC.

## Results and Limitations

Cross-validation ranked the support vector machine first (AUC 0.77), but the performance of all models lay within a single standard deviation of each other. On the held-out test set the model performed similarly (AUC 0.75), with high sensitivity (0.857) but poor specificity (0.556). For a screening tool, improved sensitivity at the cost of specificity is preferable to the alternative - a missed case is costlier than a false positive - but the model falls short of the performance required for clinical use. The clear limitation is sample size (n = 23), which can be seen in the steep steps of the ROC curve. The next step would be the validation of the pipeline on a larger cohort of these metabolites followed by hypertuning.

## Stack and Methods

Python 3.12 - pandas - numpy - scikit-learn - seaborn - matplotlib

## Reproducibility

Create the environment and launch the notebook as follows:

conda env create -f environment.yml
conda activate cachexia-ml
code cachexia_ML.ipynb

The dataset is included.

## Data

Eisner R et al. Learning to predict cancer-associated skeletal muscle wasting from ¹H-NMR profiles of urinary metabolites. Metabolomics 2011; 7:25–34. DOI: 10.1007/s11306-010-0232-9