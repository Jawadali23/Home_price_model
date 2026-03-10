# Real_state - Data Science & Model Training

Jupyter notebook containing the complete machine learning pipeline for home price prediction.

## Files

- **RealState.ipynb** - Complete ML workflow from data cleaning to model export
- **columns.json** - Feature columns metadata

## Notebook Contents

1. **Data Loading** - Import Bangalore housing dataset (~13K records)
2. **Data Cleaning** - Remove nulls, handle inconsistent data
3. **Feature Engineering** - Extract BHK, create price_per_sqft, consolidate locations
4. **Outlier Removal** - Business logic, statistical, and domain-based filtering
5. **Model Training** - Compare LinearRegression, Lasso, DecisionTree using GridSearchCV
6. **Model Export** - Save model as pickle and columns as JSON

## Model Output

- `banglore_home_prices_model.pickle` - Trained Linear Regression model
- `columns.json` - Feature names for prediction (241 locations + 3 numerical features)

## Results

- **Algorithm:** Linear Regression
- **Accuracy:** ~84% R² (5-fold cross-validation)
- **Features:** 244 total (sqft, bath, bhk + 241 one-hot encoded locations)
- **Final Dataset:** ~7K records after cleaning

## Requirements

```bash
pip install pandas numpy matplotlib scikit-learn jupyter
```

## Run

```bash
jupyter notebook RealState.ipynb
```

