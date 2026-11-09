# Osteoporosis Risk Classification: Random Forest vs. XGBoost with SHAP

Code accompanying the manuscript *"Random Forest and XGBoost Comparison Using SHAP for Osteoporosis Risk Classification"* (under revision at *Sinkron: Jurnal dan Penelitian Teknik Informatika*).

The notebook compares Random Forest and XGBoost for classifying the osteoporosis-risk label of a public lifestyle dataset. Both models are evaluated under identical conditions (stratified train-test split, GridSearchCV tuning, a robustness test in which tuning is repeated on every split, and an age-only comparison) and interpreted with SHAP computed on the tuned models.

## Authors

Ibni Faiq Athallah, Irawan, Marrylinteri Istoningtyas (Universitas Dinamika Bangsa, Jambi, Indonesia)

## Dataset

[Lifestyle Factors Influencing Osteoporosis](https://www.kaggle.com/datasets/amitvkulkarni/lifestyle-factors-influencing-osteoporosis) (Kulkarni, 2023), 1,958 records and 15 attributes after removing the `Id` column. The dataset is **not redistributed** in this repository; the notebook downloads it with `kagglehub`. Please check the dataset page for its license and terms of use. The dataset description does not state how the osteoporosis label was assigned, so results describe how well the models reproduce the dataset label, not clinical diagnosis.

## Repository contents

| File | Description |
|---|---|
| `Osteoporosis.ipynb` | Full pipeline: data loading and cleaning, encoding, baseline and tuned models, per-split re-tuning, age-only comparison, threshold evaluation, SHAP analysis, and an appendix with individual-prediction demos |
| `requirements.txt` | Python dependencies, pinned to the versions used to produce the reported results |
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

All random processes are seeded (`random_state`), so results should reproduce with the pinned library versions. Re-tuning on every split takes several minutes.

## Main results (accuracy)

| Evaluation | Random Forest | XGBoost |
|---|---|---|
| Baseline, test set of split 42 | 82.65% | 85.97% |
| Tuned, test set of split 42 | 83.67% | 88.27% |
| Re-tuned on each split, mean ± SD over 5 random states | 85.82% ± 1.77% | 91.33% ± 1.92% |
| Age only (no tuning), mean ± SD over 5 random states | 88.47% ± 1.32% | 91.48% ± 1.86% |

Notes:

- XGBoost is more accurate than Random Forest in all five random states, but its variation across splits is not smaller (SD 1.92% vs. 1.77%).
- Models that use only age reach accuracy comparable to the 18-feature models: in this dataset all records aged 39 or older are labeled at-risk, and the classes overlap only at age 38 or younger. The other 17 features did not add measurable predictive value beyond age.
- SHAP values are computed on the tuned models using the test set of split 42. Random Forest values are on the probability scale and XGBoost values on the log-odds scale, so feature rankings and relative shares are compared instead of raw values.

## Citation

If you use this code, please cite the manuscript (details will be added after publication):

```
Athallah, I. F., Irawan, & Istoningtyas, M. (2026). Random Forest and XGBoost Comparison Using SHAP for Osteoporosis Risk Classification. Sinkron: Jurnal dan Penelitian Teknik Informatika.
```

## License

Released under the MIT License (see `LICENSE`).
