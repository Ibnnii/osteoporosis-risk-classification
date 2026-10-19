# Osteoporosis Risk Classification: Random Forest vs. XGBoost with SHAP

Code accompanying the manuscript *"Random Forest and XGBoost Comparison Using SHAP for Osteoporosis Risk Classification"* (submitted to *Sinkron: Jurnal dan Penelitian Teknik Informatika*).

The notebook compares Random Forest and XGBoost for classifying osteoporosis risk from lifestyle, hormonal, and medical-history attributes. Both models are evaluated under identical conditions (single stratified split, 5-fold cross-validation, GridSearchCV tuning, and a robustness test over five random states), and interpreted with SHAP.

## Authors

Ibni Faiq Athallah, Marrylinteri Istonigtyas, Irawan (Universitas Dinamika Bangsa, Jambi, Indonesia)

## Dataset

[Lifestyle Factors Influencing Osteoporosis](https://www.kaggle.com/datasets/amitvkulkarni/lifestyle-factors-influencing-osteoporosis) (Kulkarni, 2023), 1,958 records and 15 attributes after removing the `Id` column. The dataset is **not redistributed** in this repository; the notebook downloads it with `kagglehub`. Please check the dataset page for its license and terms of use.

## Repository contents

| File | Description |
|---|---|
| `Osteoporosis.ipynb` | Full pipeline: data loading and cleaning, encoding, baseline models, cross-validation, hyperparameter tuning, robustness test, SHAP analysis, and an appendix with individual-prediction demos |
| `requirements.txt` | Python dependencies |
| `figures/` | Figures exported by the notebook |

## How to run

**Google Colab (easiest):** open `Osteoporosis.ipynb` in Colab and run all cells from top to bottom.

**Locally:**

```bash
git clone https://github.com/Ibnnii/osteoporosis-risk-classification.git
cd osteoporosis-risk-classification
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook Osteoporosis.ipynb
```

## Main results (held-out test set, `random_state = 42`)

| Model | Baseline accuracy | Tuned accuracy | Mean accuracy over 5 random states |
|---|---|---|---|
| Random Forest | 83% | 84% | 85.92% ± 1.67% |
| XGBoost | 86% | 88% | 91.43% ± 1.96% |

Notes:

- Baseline 5-fold cross-validation is run on the full dataset; the tuned cross-validation score (GridSearchCV best score) is computed within the training set only.
- Hyperparameters used in the robustness test were selected on the training portion of the `random_state = 42` split, so the other four random states may be slightly optimistic (see the Limitations section of the manuscript).
- SHAP values are computed for the baseline (untuned) models on the test set.

## Citation

If you use this code, please cite the manuscript (details will be added after publication):

```
Athallah, I. F., Istonigtyas, M., & Irawan. (2026). Random Forest and XGBoost Comparison Using SHAP for Osteoporosis Risk Classification. Sinkron: Jurnal dan Penelitian Teknik Informatika.
```

## License

Released under the MIT License (see `LICENSE`).
