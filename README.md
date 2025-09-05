# Interpretable Alzheimer's Classification Using Gradient Boosting, SHAP, and LIME

## Introduction

Alzheimer's disease (AD) is the most common cause of dementia, responsible for nearly 70% of cases worldwide. Early detection is challenging because symptoms typically appear only after significant brain damage. This project investigates whether interpretable machine learning methods can accurately classify AD while also providing explanations that clinicians can trust. The aim is not just prediction but transparency, making the models useful in real-world medical decision-making.

## Motivation

Traditional diagnostic methods such as brain imaging are costly and often fail to detect early-stage AD. Machine learning offers a cost-effective alternative by identifying hidden patterns in demographic, clinical, and imaging data. Interpretable models, in particular, highlight which features drive predictions, offering both diagnostic accuracy and actionable insights for doctors. This balance could support earlier intervention and reduce the societal burden of AD.

## Background

Alzheimer's was first identified in the early 1900s by Dr. Alois Alzheimer, who discovered amyloid plaques and neurofibrillary tangles as hallmarks of the disease. With modern imaging and computational tools, researchers can now analyze these patterns more effectively. Prior studies have shown machine learning models like Random Forests and SVMs achieve high accuracy but often act as "black boxes." Inspired by Kwan et al. (2025), who combined gradient boosting with SHAP explanations, I extend their approach with a deeper focus on interpretability.

## Dataset

The dataset used is from the Kaggle, containing 373 samples with features spanning demographics, cognitive assessments, and neuroimaging measures. Key attributes include:

- **CDR (Clinical Dementia Rating)** – severity of dementia
- **MMSE (Mini-Mental State Examination)** – cognitive test
- **eTIV (Estimated Total Intracranial Volume)** – brain size
- **nWBV (normalized Whole Brain Volume)** – brain volume proportion
- **ASF (Atlas Scaling Factor)** – MRI scaling adjustment

These features capture both functional and structural aspects of AD progression.

## Models

The experiment is done with three gradient boosting classifiers: XGBoost, LightGBM, and CatBoost. These models were chosen for their efficiency with tabular data and ability to capture nonlinear feature relationships. CatBoost, in particular, handles categorical variables effectively, while XGBoost and LightGBM optimize for speed and scalability.

## Evaluation Metrics

Because the dataset is imbalanced, Precision, Recall, F1-score, and AUC are used instead of accuracy alone. Recall and F1 were prioritized, since missing a dementia case (false negative) is more harmful than raising a false alarm. Stratified repeated cross-validation was applied to ensure balanced evaluation across folds.

## Interpretability

Feature importance is employed using SHAP, and LIME to interpret model predictions. SHAP provided global insights into feature influence, while LIME explained individual cases. Results consistently showed nWBV, eTIV, and education as strong predictors, while SES contributed little and often introduced false negatives. These insights guided iterative feature selection across experiments.

## Experiments

Experiments conducted:

1. **Baseline replication** – confirmed CDR and MMSE dominated predictions.
2. **Removing converted class** – yielded artificially perfect results, indicating target leakage.
3. **Excluding CDR, MMSE, and ASF** – produced more modest but realistic performance.
4. **Excluding SES** – improved recall and reduced false negatives in XGBoost and CatBoost.

These steps progressively reduced bias and improved interpretability.

## Process graph

<img width="494" height="375" alt="image" src="https://github.com/user-attachments/assets/c4b105ae-91f4-4b31-a188-c818dbe57c0f" />


## Results

After removing problematic features, models achieved 86–88% accuracy, 80–86% recall, 84–92% precision, and 91–96% AUC. Among the three, CatBoost consistently provided the best balance of accuracy, recall, and robustness. Importantly, SHAP and LIME revealed systematic errors and guided feature refinements, proving the value of interpretable AI in healthcare.

## Conclusion

This study shows that interpretable machine learning can support Alzheimer's classification without sacrificing transparency. While features like CDR and MMSE inflate performance unfairly, focusing on structural and demographic predictors yields clinically meaningful insights. CatBoost emerged as the most reliable model, and interpretability methods revealed both strengths and pitfalls in prediction.

## Limitations & Future Work

The dataset size was small, limiting generalizability. Future research should expand to larger cohorts such as ADNI, incorporate longitudinal and multimodal data (MRI, PET, genetics), and address fairness issues across subgroups. Building more robust, bias-aware models will be crucial for clinical deployment.
