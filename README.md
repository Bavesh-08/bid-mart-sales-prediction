<div align="center">

```
██████╗ ██╗ ██████╗ ███╗   ███╗ █████╗ ██████╗ ████████╗
██╔══██╗██║██╔════╝ ████╗ ████║██╔══██╗██╔══██╗╚══██╔══╝
██████╔╝██║██║  ███╗██╔████╔██║███████║██████╔╝   ██║   
██╔══██╗██║██║   ██║██║╚██╔╝██║██╔══██║██╔══██╗   ██║   
██████╔╝██║╚██████╔╝██║ ╚═╝ ██║██║  ██║██║  ██║   ██║   
╚═════╝ ╚═╝ ╚═════╝ ╚═╝     ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝   ╚═╝   
```

### 🛒 BigMart Sales Prediction

## 📌 Overview

This project builds a **machine learning regression model** to predict sales of products across various BigMart outlets. Using real-world retail data with 8,523 records, the model learns patterns from product attributes and outlet characteristics to forecast `Item_Outlet_Sales`.

> 🎯 **Goal:** Help retail chains optimize inventory, understand sales drivers, and make data-informed business decisions.

---

## 📊 Dataset

| Feature | Description |
|---|---|
| `Item_Identifier` | Unique product ID |
| `Item_Weight` | Weight of the product |
| `Item_Fat_Content` | Low Fat / Regular |
| `Item_Visibility` | % display area in store |
| `Item_Type` | Product category |
| `Item_MRP` | Maximum retail price |
| `Outlet_Identifier` | Unique store ID |
| `Outlet_Establishment_Year` | Year the outlet was established |
| `Outlet_Size` | Store size (Small / Medium / High) |
| `Outlet_Location_Type` | Tier 1 / 2 / 3 city |
| `Outlet_Type` | Grocery Store / Supermarket |
| `Item_Outlet_Sales` | ⭐ **Target variable** |

- **Total Records:** 8,523  
- **Total Features:** 12 (11 input + 1 target)

---

## 🔧 Project Workflow

```
Raw Data  ──►  Data Cleaning  ──►  EDA  ──►  Encoding  ──►  Model Training  ──►  Evaluation
```

### 1️⃣ Data Cleaning
- Filled **1,463 missing** `Item_Weight` values with the **column mean**
- Filled **2,410 missing** `Outlet_Size` values using **mode per Outlet Type** via pivot table
- Standardized `Item_Fat_Content` labels: `'low fat'`, `'LF'` → `'Low Fat'` | `'reg'` → `'Regular'`

### 2️⃣ Exploratory Data Analysis
Plotted distributions of all key numerical features:
- `Item_Weight` — fairly uniform distribution
- `Item_Visibility` — right-skewed (many items have near-zero visibility)
- `Item_MRP` — multimodal pricing tiers
- `Item_Outlet_Sales` — right-skewed target variable
- `Outlet_Establishment_Year` — sparse across decades

### 3️⃣ Feature Encoding
Applied **Label Encoding** to all categorical columns:
`Item_Identifier`, `Item_Fat_Content`, `Item_Type`, `Outlet_Identifier`, `Outlet_Size`, `Outlet_Location_Type`, `Outlet_Type`

### 4️⃣ Train-Test Split
```python
x_train, x_test, y_train, y_test = train_test_split(x, y, test_size=0.2, random_state=2)
# Train: 6818 samples | Test: 1705 samples
```

### 5️⃣ Model — XGBoost Regressor
```python
from xgboost import XGBRegressor
model = XGBRegressor()
model.fit(x_train, y_train)
```

---

## 📈 Results

| Dataset | R² Score |
|---|---|
| 🟢 Training Set | **0.8774** |
| 🔵 Test Set | **0.5120** |

> The model explains ~**87.7%** of the variance in training data and ~**51.2%** on unseen test data. The gap suggests room for hyperparameter tuning and feature engineering improvements.

---

## 🛠️ Tech Stack

| Library | Purpose |
|---|---|
| `pandas` | Data loading & manipulation |
| `numpy` | Numerical operations |
| `matplotlib` / `seaborn` | Data visualization |
| `scikit-learn` | Preprocessing, train-test split, metrics |
| `xgboost` | Gradient boosted regression model |

---

## 🚀 Getting Started

### Prerequisites
```bash
pip install numpy pandas matplotlib seaborn scikit-learn xgboost
```

### Run the Notebook
```bash
# Clone the repo
git clone https://github.com/your-username/bigmart-sales-prediction.git
cd bigmart-sales-prediction

# Open in Jupyter or Google Colab
jupyter notebook BigMart_Sales_Prediction.ipynb
```

> 💡 You can also open directly in **Google Colab** using the badge at the top.

---

## 📁 Project Structure

```
bigmart-sales-prediction/
│
├── 📓 BigMart_Sales_Prediction.ipynb   # Main notebook
├── 📄 bigmart.csv                       # Dataset
└── 📘 README.md                         # You are here
```

---

## 🔮 Future Improvements

- [ ] Hyperparameter tuning with `GridSearchCV`
- [ ] Try ensemble models (Random Forest, LightGBM)
- [ ] Feature engineering (outlet age, item visibility bins)
- [ ] Cross-validation for robust evaluation
- [ ] Deploy as a web app using Streamlit or Flask

---

## 🙋 Author

<div align="center">

**Built with ❤️ using Python & XGBoost**

*Feel free to ⭐ star this repo if you found it helpful!*

</div>
