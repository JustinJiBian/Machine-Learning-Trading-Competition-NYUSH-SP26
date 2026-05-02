# CSI500 Quantitative Equity Portfolio Generation

This repository contains the end-to-end pipeline for a high-alpha equity portfolio (CSI500 universe). The model utilizes a **Domain-Specific Sub-Ensemble of XGBRankers** and an **Exponential Conviction Allocator** to achieve a significant outperformance over the competition baseline.

## 🚀 Performance Summary
- **Excess Return over Baseline:** +173.48 BPS (Out-of-Sample)
- **Framework:** Learning-to-Rank (Pairwise)
- **Diversification:** 50 stocks (Max weight 10%, Min weight per competition rules)

## 🛠 Installation & Setup

0. **Fastest way to reproduce the result**:
Download Stock_competition.ipynb and run all cell in Google Colab, the hyperparameters and random seeds are in the file as well as below.

1. **Clone the official competition repo first** (to get data utilities):
   ```bash
   git clone [https://github.com/NYUSH-ML/ml-competition-sp26.git](https://github.com/NYUSH-ML/ml-competition-sp26.git)
   cd ml-competition-sp26

2. Install Dependencies:
   ```bash
   pip install -r requirements.txt
   pip install xgboost lightgbm catboost

3. Download/Update Data:
Ensure your data is updated to the latest available date used in the report (May 2, 2026):
   ```bash
   python download_data.py --start 20250101 --end 20260502

🔄 How to Reproduce Results
To reproduce the exact portfolio uploaded to Gradescope:

Open Stock_competition.ipynb in Jupyter or Google Colab.

Ensure the CONFIG dictionary matches the values in the table below.

Run all cells chronologically.

The final cell will generate submission_final_for_real.csv, which matches the submitted file.

⚙️ Reproducibility Configuration
The following parameters are hardcoded in the CONFIG dictionary to ensure deterministic results.
```bash
Parameter,Value,Description
random_seed,42,Ensures deterministic XGBoost splits
n_estimators,1500,Tree count for ensemble experts
learning_rate,0.03,Shrinkage factor
max_depth,4,Shallow trees to prevent overfitting
decay_factor,0.001,Critical: Controls portfolio conviction
oos_test_days,20,Evaluation window length
embargo_days,5,Prevents look-ahead leakage

Developed with the assistance of Google Gemini 3.1 Pro.
