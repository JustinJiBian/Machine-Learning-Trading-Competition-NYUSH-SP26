# CSI500 Quantitative Equity Portfolio Generation

This repository contains the end-to-end pipeline for a high-alpha equity portfolio (CSI500 universe). The model utilizes a **Domain-Specific Sub-Ensemble of XGBRankers** and an **Exponential Conviction Allocator** to achieve a significant outperformance over the competition baseline.

## 🚀 Performance Summary
- **Excess Return over Baseline:** +173.48 BPS (Out-of-Sample)
- **Framework:** Learning-to-Rank (Pairwise)
- **Diversification:** 50 stocks (Max weight 10%, Min weight per competition rules)

## 🛠 Installation & Setup

1. **Clone the official competition repo first** (to get data utilities):
   ```bash
   git clone [https://github.com/NYUSH-ML/ml-competition-sp26.git](https://github.com/NYUSH-ML/ml-competition-sp26.git)
   cd ml-competition-sp26

2. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   pip install xgboost lightgbm catboost

3. **Download/Update Data**:
Ensure your data is updated to the latest available date used in the report (May 2, 2026):
   ```bash
   python download_data.py --start 20250101 --end 20260502

## 🔄 How to Reproduce Results
To reproduce the exact portfolio uploaded to Gradescope:

Open Stock_competition.ipynb in Jupyter or Google Colab.

Ensure the CONFIG dictionary matches the values in the table below.

Run all cells chronologically.

The final cell will generate submission_final_for_real.csv, which matches the submitted file.

## ⚙️ Model Hyperparameters & Reproducibility

To ensure the +173.48 BPS result is reproducible, the following configuration must be used. These parameters are centralized in the `CONFIG` dictionary within the notebook.

| Category | Hyperparameter | Value | Rationale |
| :--- | :--- | :--- | :--- |
| **Model** | `n_estimators` | `1500` | High count for ensemble stability |
| | `learning_rate` | `0.03` | Optimal shrinkage for CSI500 noise |
| | `max_depth` | `4` | Prevents overfitting to outliers |
| | `objective` | `rank:pairwise` | Focuses on relative asset ordering |
| **Portfolio** | `decay_factor` ($\lambda$) | `0.001` | **Sweet spot** for diversification vs conviction |
| | `top_k` | `50` | Diversified basket size |
| | `max_w` | `0.10` | Strict compliance with 10% ceiling |
| **Pipeline** | `random_seed` | `42` | Ensures deterministic results |
| | `embargo_days` | `5` | Zero look-ahead leakage |

## Acknowledgements
Developed with the assistance of Google Gemini 3.1 Pro.
