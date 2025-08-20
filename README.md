# 🚜 Bulldozer Price Prediction

This repository contains the code for a machine learning project that predicts the sale price of bulldozers based on their usage, equipment type, and configuration. The solution is developed for the Kaggle competition "[Blue Book for Bulldozers](https://www.kaggle.com/c/bluebook-for-bulldozers)".

The project uses a Random Forest Regressor and includes a comprehensive data preprocessing pipeline to handle the complex, time-series dataset provided.

---

## 📊 Dataset

The data for this project is sourced from the Kaggle competition and is not included in this repository due to its size. You can download it directly from the **[competition page](https://www.kaggle.com/c/bluebook-for-bulldozers/data)**.

After downloading, you must place the `.csv` files inside a subfolder named `bluebook-for-bulldozers` for the notebook to run correctly.

---

## ⚙️ Methodology

The project follows a structured machine learning workflow:

1.  **Data Preprocessing & Feature Engineering**:
    * The `saledate` column is parsed to extract temporal features like `saleYear`, `saleMonth`, and `saleDayofweek`.
    * Missing numerical values (e.g., `MachineHoursCurrentMeter`) are imputed using the median of the training data. A binary indicator column (`_is_missing`) is also created to retain the information that a value was originally missing.
    * All object-type columns are converted to pandas `category` types, which are then converted into numerical codes for the model. This process ensures consistent encoding across the training, validation, and test sets.

2.  **Target Transformation**:
    * To optimize for the competition's Root Mean Squared Log Error (RMSLE) metric, the target variable `SalePrice` is transformed using `np.log1p` before training. Predictions are converted back to their original scale using `np.expm1`.

3.  **Model Training & Hyperparameter Tuning**:
    * A `RandomForestRegressor` is used as the predictive model.
    * Hyperparameter tuning is performed using `RandomizedSearchCV`.
    * To prevent data leakage in the time-series data, a `TimeSeriesSplit` is used as the cross-validation strategy during tuning.

4.  **Final Model Training**:
    * After identifying the best hyperparameters, the model is retrained on the **combined training and validation datasets** to learn from all available data before making final predictions on the test set.

---

## 🚀 How to Run

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/AkshatJ24/Bulldozer-Price-Prediction.git](https://github.com/AkshatJ24/Bulldozer-Price-Prediction.git)
    ```
2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
3.  **Download the data:** Download the competition data from [Kaggle](https://www.kaggle.com/c/bluebook-for-bulldozers/data) and place it in the required folder structure as shown below.

4.  **Run the notebook:** Open and run the `Bulldozer Price Prediction.ipynb` notebook to execute the full data processing and model training pipeline.

---

## 📁 File Structure
├── bluebook-for-bulldozers/  <- You need to create this and add the data
│   ├── TrainAndValid.csv
│   ├── Test.csv
│   └── ... (other data files)
│
├── bulldozer_price_predictions_optimized.csv   <- The generated submission file
├── Bulldozer Price Prediction.ipynb            <- The main notebook with all the code
├── requirements.txt                            <- Required Python libraries
└── README.md                                   <- This file
