# 🏠 Bangalore Home Price Prediction

End-to-end ML project predicting Bangalore home prices using Linear Regression, Flask REST API, and interactive web interface.

## 🎯 Overview

Full-stack machine learning application for real estate price prediction based on area, BHK, bathrooms, and location (241+ locations in Bangalore).

**Stack:** Python ML Model → Flask API → HTML/CSS/JS Frontend | **Accuracy:** ~84% R²

## 🛠️ Tech Stack

**ML:** Python, Pandas, NumPy, Matplotlib, Scikit-learn (LinearRegression, GridSearchCV)  
**Backend:** Flask, Pickle  
**Frontend:** HTML5, CSS3, JavaScript, jQuery

## 📁 Project Structure

```
Home_price_model/
│
├── Real_state/                      # Data Science & Model Development
│   ├── RealState.ipynb             # Jupyter notebook with complete ML pipeline
│   ├── columns.json                # Feature columns for the model
│   └── bengaluru_house_prices.csv  # Original dataset (not included)
│
├── Server/                          # Flask Backend
│   ├── server.py                   # Flask REST API server
│   ├── util.py                     # Utility functions for predictions
│   └── Artifacts/                  # Model artifacts
│       ├── banglore_home_prices_model.pickle  # Trained model
│       └── columns.json            # Location and feature names
│
└── Client/                          # Frontend Web Application
    ├── app.html                    # Main HTML interface
    ├── app.css                     # Styling
    └── app.js                      # JavaScript for API calls
```

## 🚀 Quick Start

```bash
# Install dependencies
pip install pandas numpy matplotlib scikit-learn flask

# Run server
cd Server
python server.py

# Open Client/app.html in browser
```

## 💡 Usage

**Web Interface:** Open `Client/app.html` → Enter sqft, BHK, bathrooms, location → Get price estimate (in Lakhs)

**API:**
```bash
# Get locations
curl http://127.0.0.1:5000/get_location_names

# Predict price
curl -X POST http://127.0.0.1:5000/predict_home_price \
  -H "Content-Type: application/json" \
  -d '{"total_sqft": 1000, "location": "1st phase jp nagar", "bhk": 2, "bath": 2}'
```

## 🔬 Data Science Pipeline

**1. Data Cleaning** (~13K → 7K records)
- Removed unnecessary columns, handled missing values
- Converted range sqft values (e.g., "1000-1200" → 1100)
- Consolidated 1300+ locations to 241 meaningful ones

**2. Feature Engineering**
- Extracted `bhk` from size column
- Created `price_per_sqft` for outlier detection
- One-hot encoded locations (241 features)

**3. Outlier Removal**
- Business logic: sqft/BHK < 300
- Statistical: mean ± 1 std deviation per location
- Domain knowledge: 2 BHK > 3 BHK price, bathrooms > BHK+2

**4. Model Selection** (GridSearchCV comparison)
- **Linear Regression** ✅ Selected (R² ~ 0.84)
- Lasso Regression
- Decision Tree Regressor

**5. Evaluation**
- 5-fold cross-validation (80-20 split)
- 244 features (3 numerical + 241 location dummies)
- Mean R² score: ~84%

## 🚀 Future Enhancements

- Add features (property age, amenities, parking)
- Deep learning models, mobile app
- Cloud deployment (AWS/Azure/GCP)
- Price trend dashboard, multi-city support

## 📚 Key Learnings

**Data Science:** Data cleaning, feature engineering, outlier detection, model selection (GridSearchCV), cross-validation

**Engineering:** REST API development, full-stack integration, modular architecture, production-ready code structure

## 📝 License

MIT License - Open source and free to use.

---

⭐ **Star this repo if you found it helpful!**

**Note:** Educational project demonstrating complete ML workflow. Not for actual real estate transactions without validation.

**Note**: This project is for educational purposes and demonstrates a complete machine learning workflow. The model's predictions should not be used for actual real estate transactions without further validation and updates with current market data.
