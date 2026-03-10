# 🏠 Bangalore Home Price Prediction Model

A complete end-to-end machine learning project that predicts home prices in Bangalore based on area, number of bedrooms (BHK), bathrooms, and location. This project includes data science model building, a Flask REST API backend, and an interactive web interface.

## 📋 Table of Contents
- [Project Overview](#project-overview)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Data Science Pipeline](#data-science-pipeline)
- [Model Performance](#model-performance)
- [API Endpoints](#api-endpoints)
- [Future Enhancements](#future-enhancements)
- [Learning Outcomes](#learning-outcomes)

## 🎯 Project Overview

This project demonstrates a full-stack machine learning application for predicting real estate prices in Bangalore. The model is trained on historical housing data and provides price estimates based on property features.

**Key Components:**
- **Data Science Model**: Built using Linear Regression with extensive data cleaning and outlier removal
- **Backend Server**: Flask REST API that serves predictions
- **Frontend**: Interactive HTML/CSS/JavaScript web interface for user input

## ✨ Features

- 🏘️ **Predict home prices** based on:
  - Total square feet area
  - Number of bedrooms (BHK)
  - Number of bathrooms
  - Location in Bangalore (241+ locations)

- 📊 **Data-driven insights** from Bangalore housing market
- 🎨 **User-friendly web interface** with responsive design
- 🔄 **Real-time predictions** via REST API
- 📈 **Model accuracy**: ~84% R² score using cross-validation

## 🛠️ Technologies Used

### Data Science & Machine Learning
- **Python 3.x**
- **Pandas** - Data manipulation and analysis
- **NumPy** - Numerical computations
- **Matplotlib** - Data visualization
- **Scikit-learn** - Machine learning algorithms
  - Linear Regression (selected model)
  - Lasso Regression
  - Decision Tree Regressor
  - GridSearchCV for hyperparameter tuning
  - Cross-validation for model evaluation

### Backend
- **Flask** - Web framework for REST API
- **Pickle** - Model serialization
- **JSON** - Data exchange format

### Frontend
- **HTML5** - Structure
- **CSS3** - Styling with Google Fonts
- **JavaScript** - Interactivity
- **jQuery** - AJAX requests and DOM manipulation

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

## 🚀 Installation

### Prerequisites
- Python 3.7 or higher
- pip package manager
- Web browser (Chrome, Firefox, etc.)

### Setup Instructions

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/home-price-prediction.git
cd home-price-prediction
```

2. **Install Python dependencies**
```bash
pip install pandas numpy matplotlib scikit-learn flask
```

3. **Navigate to the server directory**
```bash
cd Server
```

4. **Run the Flask server**
```bash
python server.py
```
The server will start on `http://127.0.0.1:5000/`

5. **Open the web interface**
- Navigate to the `Client` folder
- Open `app.html` in your web browser

## 💡 Usage

### Using the Web Interface

1. **Open** `Client/app.html` in your browser
2. **Enter** the property details:
   - Area in square feet (e.g., 1000)
   - Select BHK (1-5 bedrooms)
   - Select number of bathrooms (1-5)
   - Choose location from dropdown
3. **Click** "Estimate Price"
4. **View** the predicted price in Lakhs (1 Lakh = 100,000 INR)

### Using the API Directly

**Get all locations:**
```bash
curl http://127.0.0.1:5000/get_location_names
```

**Predict home price:**
```bash
curl -X POST http://127.0.0.1:5000/predict_home_price \
  -H "Content-Type: application/json" \
  -d '{
    "total_sqft": 1000,
    "location": "1st phase jp nagar",
    "bhk": 2,
    "bath": 2
  }'
```

## 🔬 Data Science Pipeline

The model development follows a comprehensive data science workflow:

### 1. **Data Loading**
- Dataset: Bangalore house prices with ~13,000 records
- Features: area_type, location, size, total_sqft, bath, balcony, price

### 2. **Data Cleaning**
- Removed unnecessary columns (area_type, society, availability, balcony)
- Handled missing values using `dropna()`
- Stripped whitespace from location names
- Converted range values in `total_sqft` to numeric (e.g., "1000-1200" → 1100)

### 3. **Feature Engineering**

**Created new features:**
- `bhk` - Extracted bedroom count from size column (e.g., "2 BHK" → 2)
- `price_per_sqft` - Calculated price per square foot for outlier detection

**Location dimensionality reduction:**
- Consolidated locations with ≤10 data points into "other" category
- Reduced from 1,300+ locations to 241 meaningful locations

### 4. **Outlier Removal**

Applied multiple outlier removal techniques:

**a) Business Logic Outliers:**
- Removed properties where sqft/BHK < 300 (unrealistic bedroom sizes)

**b) Statistical Outliers:**
- Removed properties outside mean ± 1 standard deviation of price_per_sqft for each location

**c) Domain Knowledge Outliers:**
- Removed properties where 2 BHK price > 3 BHK price in same location
- Removed properties with bathrooms > BHK + 2 (unusual property configuration)

### 5. **Model Building**

**Preprocessing:**
- One-hot encoding for location feature (241 locations)
- Training features: total_sqft, bath, bhk, location (one-hot encoded)
- Target variable: price

**Model Selection using GridSearchCV:**

Compared three algorithms:
1. **Linear Regression** ✅ (Selected)
   - Cross-validation R² score: ~0.84
   - Best performance for this dataset
   
2. Lasso Regression
   - Tested with different alpha values and selection methods
   
3. Decision Tree Regressor
   - Tested with different criterion and splitter parameters

**Cross-Validation:**
- 5-fold Shuffle Split cross-validation
- 80-20 train-test split
- Mean R² score: ~84%

### 6. **Model Export**
- Saved trained Linear Regression model using `pickle`
- Exported feature columns to JSON for prediction pipeline

## 📊 Model Performance

- **Algorithm**: Linear Regression
- **Cross-Validation Score**: ~84% R²
- **Training/Test Split**: 80-20
- **Number of Features**: 244 (3 numerical + 241 location dummies)
- **Dataset Size**: ~7,000 records after cleaning and outlier removal

**Key Insights:**
- Location is the most significant factor in price prediction
- Price per square foot varies significantly across Bangalore locations
- Model performs well for properties with 2-3 BHK configurations
- Outlier removal improved model stability and reduced overfitting

## 🔌 API Endpoints

### 1. Get Location Names
**Endpoint:** `GET /get_location_names`

**Response:**
```json
{
  "locations": ["1st block jayanagar", "1st phase jp nagar", ...]
}
```

### 2. Predict Home Price
**Endpoint:** `POST /predict_home_price`

**Request Body:**
```json
{
  "total_sqft": 1000,
  "location": "1st phase jp nagar",
  "bhk": 2,
  "bath": 2
}
```

**Response:**
```json
{
  "estimated_price": 83.5
}
```
*Price is in Lakhs (1 Lakh = 100,000 INR)*

## 🚀 Future Enhancements

- [ ] Add more features (age of property, amenities, parking)
- [ ] Implement deep learning models for better accuracy
- [ ] Create a mobile application
- [ ] Add property comparison feature
- [ ] Integrate real-time market data
- [ ] Deploy on cloud (AWS/Azure/GCP)
- [ ] Add authentication and user profiles
- [ ] Create price trend visualization dashboard
- [ ] Implement A/B testing for model improvements
- [ ] Add support for other Indian cities

## 📚 Learning Outcomes

This project demonstrates proficiency in:

### Data Science Skills
- ✅ **Data cleaning and preprocessing** - Handling missing values, outliers, inconsistent data
- ✅ **Feature engineering** - Creating meaningful features, dimensionality reduction
- ✅ **Exploratory data analysis** - Understanding data distributions and relationships
- ✅ **Outlier detection** - Statistical and domain-based outlier removal
- ✅ **Model selection** - Comparing multiple algorithms with GridSearchCV
- ✅ **Model evaluation** - Cross-validation, R² score interpretation
- ✅ **Model persistence** - Saving and loading trained models

### Software Engineering Skills
- ✅ **REST API development** - Building Flask endpoints with CORS support
- ✅ **Full-stack development** - Integrating ML model with web application
- ✅ **Separation of concerns** - Clean code architecture (server, client, model)
- ✅ **Error handling** - Graceful handling of invalid inputs
- ✅ **Responsive design** - User-friendly web interface

### Best Practices
- ✅ **Reproducibility** - Well-documented Jupyter notebook
- ✅ **Code organization** - Modular structure with util functions
- ✅ **Version control ready** - Clear project structure for Git
- ✅ **Production considerations** - Model artifacts separate from code

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the issues page.

## 👨‍💻 Author

**Jawad**

---

⭐ If you found this project helpful, please give it a star!

## 📧 Contact

For questions or suggestions, please open an issue in the repository.

---

**Note**: This project is for educational purposes and demonstrates a complete machine learning workflow. The model's predictions should not be used for actual real estate transactions without further validation and updates with current market data.
