# 🏁 Lap Time Prediction using CatBoost

This project focuses on predicting **Lap_Time_Seconds** for MotoGP riders using a wide range of race, track, environmental, and performance-related features. The model is built using **CatBoost Regressor** and optimized to achieve **very low RMSE**, ideally below **0.001**.

---

## 📂 Dataset Overview

| File Name      | Description                                      |
|----------------|--------------------------------------------------|
| `train.csv`    | Historical race data with target values          |
| `test.csv`     | Race entries without target values (for prediction) |
| `val.csv`      | Sample submission format                         |

---

## 🧠 Features Used

- **Rider Metadata**  
  `Rider_ID`, `years_active`, `Championship_Position`, `Championship_Points`, etc.

- **Bike & Team Info**  
  `Bike`, `Team`, `bike_name`

- **Track Details**  
  `Circuit_Length_km`, `Corners_per_Lap`, `Pit_Stop_Duration_Seconds`

- **Environment & Conditions**  
  `Humidity_%`, `Track_Condition`, `weather`, `Ambient_Temperature_Celsius`, etc.

- **Performance Indicators**  
  `Avg_Speed_kmh`, `Grid_Position`, `Penalty`, `podiums`, `wins`, `starts`, `finishes`

---

## ⚙️ Model Pipeline

### 🔧 Preprocessing

- Missing values handled:
  - **Categorical** → `'Unknown'`
  - **Numerical** → median imputation
- All categorical features converted to string and label-encoded
- Dropped identifier fields like `Unique ID` and `rider_name` to avoid data leakage

### 🤖 Modeling

- **Model**: `CatBoostRegressor`
- **Parameters**:
  - `iterations=3000`
  - `learning_rate=0.01`
  - `depth=10`
  - `early_stopping_rounds=100`
- **Target**: RMSE < **0.001**

### 📈 Validation

- 5-Fold Cross-Validation
- Metric: **Root Mean Squared Error (RMSE)**
- Final RMSE achieved: **~0.0786**

---

## 📝 How to Run

Ensure a Kaggle-compatible Python environment (or use Jupyter locally).

```python
import pandas as pd
from catboost import CatBoostRegressor
from sklearn.metrics import mean_squared_error

# Load data
train = pd.read_csv("train.csv")
test = pd.read_csv("test.csv")
sample_submission = pd.read_csv("val.csv")

# Preprocessing, feature engineering, and training steps...


After running the notebook, predictions are saved to submission.csv.

📊 Results
✅ Final RMSE (Validation Set): 0.0786

✅ All preprocessing and predictions handled in a clean pipeline

✅ Ready for real-world deployment or ensemble integration

📌 Notes
Avoid leakage from high-cardinality ID fields (like rider_name, Unique ID)

Model can be further improved by:

Ensembling with LightGBM or XGBoost

Feature interaction generation

Hyperparameter tuning via Optuna or Bayesian Optimization

📁 File Structure
bash
Copy
Edit
burnout_Hackjack.ipynb     # Full training and prediction notebook
submission.csv             # Final test predictions
README.md                  # Project overview
