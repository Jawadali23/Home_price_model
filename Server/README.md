# Server - Flask REST API

Backend server providing REST API endpoints for home price predictions.

## Files

- **server.py** - Flask application with API endpoints
- **util.py** - Utility functions for loading model and making predictions
- **Artifacts/** - Model and data files
  - `banglore_home_prices_model.pickle` - Trained ML model
  - `columns.json` - Feature columns (241 locations + 3 features)

## API Endpoints

### GET `/get_location_names`
Returns list of all available locations (241 locations)

**Response:**
```json
{"locations": ["1st block jayanagar", "1st phase jp nagar", ...]}
```

### POST `/predict_home_price`
Predicts home price based on property features

**Request:**
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
{"estimated_price": 83.5}
```
*Price in Lakhs (1 Lakh = 100,000 INR)*

## How It Works

1. **Loads artifacts** on startup (model + columns)
2. **Encodes input** - Creates feature vector with one-hot encoding for location
3. **Predicts price** - Uses Linear Regression model
4. **Returns estimate** - Rounded to 2 decimal places

## Requirements

```bash
pip install flask numpy pickle
```

## Run

```bash
python server.py
```

Server starts on `http://127.0.0.1:5000/`

## CORS

CORS enabled for all origins to allow frontend access.

