#  Indian Houses Rent Prediction

##  Overview
This project focuses on **analyzing, cleaning, and preparing** a dataset of **Indian houses for rent** in order to build a predictive model for rental prices.  
It includes **data preprocessing, feature engineering, exploratory data analysis (EDA), missing value imputation, and visualization** to extract actionable insights from the dataset.

---

##  Dataset
**Source:** [Indian House Rent Dataset](https://www.kaggle.com/datasets/cat-reloaded-data-science/indian-houses-for-rent?select=Indian_House_Rent_Dataset.csv#:~:text=calendar_view_week-,Indian_House_Rent_Dataset,-.csv)  
**Shape:** `4746 rows × 12 columns`  

**Key Columns:**
- `Posted On` → Date when the property was listed
- `BHK` → Number of bedrooms, halls, and kitchens
- `Size` → Property size in square feet
- `Floor` → Current floor and total floors
- `Area Type` → Super Area or Carpet Area
- `Area Locality` → Specific locality of the property
- `City` → City where the property is located
- `Furnishing Status` → Furnished, Semi-Furnished, or Unfurnished
- `Tenant Preferred` → Bachelors, Family, or Both
- `Bathroom` → Number of bathrooms
- `Point of Contact` → Owner or Agent
- `Rent` → **Target variable**

---

##  Steps Performed

### **1) Data Cleaning & Feature Engineering**
- **Date Feature:**
  - Converted `Posted On` to datetime.
  - Extracted `Posted_Month` and dropped the constant `Year` part.
- **BHK & Size:**
  - Cleaned `BHK` column using regex to extract numeric values.
  - Converted `Size` to numerical square feet values.
- **Floor:**
  - Extracted `Current_Floor` and `Total_Floors`.
  - Standardized basements and ground floor values.
- **Area Type:**
  - Normalized inconsistent casing and merged duplicated categories.
- **Area Locality & City:**
  - Grouped rare localities under `"Other"`.
  - Cleaned noisy city names using regex.
- **Tenant Preferred:**
  - Cleaned inconsistent strings and standardized into three categories:
    - `Bachelors`
    - `Family`
    - `Bachelors/Family`
- **Bathroom:**
  - Removed unnecessary text (`Bathrooms`) and converted to numeric.
- **Point of Contact:**
  - Retained consistent categories: `Contact Owner` & `Contact Agent`.

---

### **2) Exploratory Data Analysis (EDA)**
- **Univariate Analysis**
  - Count plots for categorical features (`City`, `Furnishing Status`, `Area Type`, etc.)
- **Correlation Heatmap**
  - Found strong relationships between:
    - `Size` & `BHK`
    - `Size` & `Bathroom`
    - Moderate correlation between `Rent` & `Size`
- **Pairplots**
  - Visualized multi-feature relationships to identify patterns and clusters.

---

### **3) Handling Missing Values**
- **BHK** → Filled with median values.
- **Bathroom** → Filled based on median bathrooms grouped by BHK.
- **Size** → Filled by median size grouped by BHK.
- **City & Area Locality** → Imputed using mode values within each city/locality group.
- **Area Type** → Imputed using **KNN Imputer** based on similarity with BHK & Size.
- **Furnishing Status** → Filled based on the most common furnishing type in the same city.
- **Tenant Preferred** → Imputed using KNN based on BHK & Bathroom values.
- **Point of Contact** → Filled using mode within each city.

---

### **4) Encoding categorical variables** using Target and Label Encoding.

-----

### **5) Model Building & Evaluation**

We tested multiple regression models to predict **Rent**.  
Models were evaluated using **R² Score**, **Mean Absolute Error (MAE)**, and **Root Mean Squared Error (RMSE)**.

| **Model**           | **R² Score** | **MAE**   | **RMSE**   |
|---------------------|-------------|-----------|------------|
| **CatBoost**        | **0.8152**  | **5735.74** | **8463.55** |
| **LightGBM**        | 0.80995     | 5823.38   | 8583.14    |
| **Gradient Boosting** | 0.79640   | 6104.50   | 8883.80    |
| **Random Forest**   | 0.79113     | 6037.46   | 8997.99    |
| **XGBoost**         | 0.78318     | 6149.30   | 9167.77    |
| **Extra Trees**     | 0.77447     | 6218.29   | 9349.92    |
| **Decision Tree**   | 0.56802     | 8210.58   | 12940.20   |
---

### **Best Performing Model**
The **CatBoost Regressor** performed best with:
- **R² Score:** `0.815`
- **MAE:** `~5736`
- **RMSE:** `~8464`

We selected **CatBoost** as the **final model** After **hyperparameter tuning** due to its superior accuracy and stability.

---

##  Tech Stack
- **Languages:** Python  
- **Libraries:** Pandas, NumPy, Matplotlib, Seaborn  
- **Machine Learning:** Scikit-learn, XGBoost, LightGBM, CatBoost  
- **Imputation & Encoding:** KNNImputer, TargetEncoder  
- **Visualization:** Seaborn, Matplotlib  

---

[Kaggle profile](https://www.kaggle.com/reemalbadwii) 
