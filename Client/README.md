# Client - Web Interface

Interactive web application for predicting Bangalore home prices.

## Files

- **app.html** - Main interface with input forms and result display
- **app.css** - Styling with responsive design and custom radio buttons
- **app.js** - JavaScript for API calls and user interactions

## Usage

1. **Run the Flask server** (from Server directory)
   ```bash
   cd ../Server
   python server.py
   ```

2. **Open** `app.html` in your web browser

3. **Enter details:**
   - Area in square feet
   - Select BHK (1-5)
   - Select bathrooms (1-5)
   - Choose location from dropdown

4. **Click "Estimate Price"** to get prediction in Lakhs

## Features

- Real-time price predictions via AJAX
- Dynamic location dropdown populated from API
- Responsive radio button design
- Clean, user-friendly interface

## API Endpoints Used

- `GET /get_location_names` - Loads locations on page load
- `POST /predict_home_price` - Returns estimated price

## Requirements

- Modern web browser (Chrome, Firefox, Edge)
- Running Flask server on `http://127.0.0.1:5000`
