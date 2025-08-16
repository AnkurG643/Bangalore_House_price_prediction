# 🏠 Rooflyzer - Real Estate Price Prediction Web App

**Smart property price predictions powered by machine learning**

Rooflyzer is a Flask-based web application that predicts real estate prices using machine learning. Built with a Ridge regression model, it provides accurate price estimates based on property location, size, and amenities.

## 🚀 Features

### 🏘️ Location-Based Predictions
- Dynamic location dropdown with real property areas
- Location-specific price modeling for accurate predictions
- Comprehensive coverage of various neighborhoods and localities

### 🏡 Property Analysis
- **BHK Configuration**: Bedroom, hall, kitchen count analysis
- **Bathroom Count**: Impact of bathroom quantity on pricing
- **Square Footage**: Total area consideration for price calculation
- **Instant Predictions**: Real-time price estimation via web interface

### 🤖 Machine Learning Integration
- Pre-trained Ridge regression model for robust predictions
- Data preprocessing pipeline for consistent input handling
- Model persistence using pickle for efficient deployment

## 🛠️ Installation

### Prerequisites
- Python 3.7 or higher
- pip package manager

### Required Packages
```bash
pip install flask pandas pickle numpy scikit-learn
```

Or create a `requirements.txt` file:
```
Flask==2.3.2
pandas==2.0.3
numpy==1.24.3
scikit-learn==1.3.0
```

Then install:
```bash
pip install -r requirements.txt
```

### Required Files
Ensure these files are in your project directory:
- `clean_data.csv` - Processed real estate dataset
- `RidgeModel.pkl` - Trained Ridge regression model
- `templates/index.html` - Frontend template

## 📁 Project Structure

```
rooflyzer/
├── app.py                 # Main Flask application
├── RidgeModel.pkl         # Trained machine learning model
├── clean_data.csv         # Cleaned dataset for location extraction
├── templates/
│   └── index.html         # Web interface template
├── static/               # CSS, JS, images (if any)
├── requirements.txt      # Python dependencies
└── README.md            # This file
```

## 🚀 Usage

### Running the Application
1. **Start the Flask server:**
   ```bash
   python app.py
   ```

2. **Access the web interface:**
   - Open your browser and go to `http://localhost:5000`
   - The application will run on port 5000 by default

### Making Predictions
1. **Select Location**: Choose from the dropdown of available locations
2. **Enter Property Details**:
   - Number of bedrooms (BHK)
   - Number of bathrooms
   - Total square footage
3. **Get Prediction**: Click predict to get the estimated price

### API Endpoints

#### GET /
- **Purpose**: Renders the main page with location options
- **Returns**: HTML template with available locations

#### POST /predict
- **Purpose**: Processes prediction request
- **Parameters**:
  - `location`: Property location (string)
  - `bhk`: Number of bedrooms (float)
  - `bath`: Number of bathrooms (float)  
  - `sqft`: Total square footage (string/float)
- **Returns**: Predicted price as a rounded number

## 🧠 Machine Learning Model

### Model Details
- **Algorithm**: Ridge Regression
- **Purpose**: Linear regression with L2 regularization
- **Benefits**: 
  - Handles multicollinearity well
  - Reduces overfitting
  - Stable predictions for real estate data

### Data Features
The model uses these key features:
- **Location**: Categorical feature representing property area
- **Total Square Feet**: Continuous variable for property size
- **BHK**: Number of bedrooms (discrete)
- **Bathrooms**: Number of bathrooms (discrete)

### Prediction Output
- Raw prediction is multiplied by 1e5 (100,000) for proper scaling
- Final output is rounded to 2 decimal places
- Represents estimated property price in the dataset's currency unit

## 💻 Technical Implementation

### Data Processing
```python
# Input preprocessing
input = pd.DataFrame([[locations, sqft, bhk, bath]], 
                    columns=['location', 'total_sqft', 'bhk', 'bath'])

# Prediction with scaling
prediction = pipe.predict(input)[0] * 1e5
```

### Model Pipeline
The `RidgeModel.pkl` file contains a complete preprocessing and prediction pipeline that handles:
- Feature encoding for categorical variables
- Numerical feature scaling
- Ridge regression prediction

## 🔧 Customization

### Adding New Features
1. Update the HTML form in `templates/index.html`
2. Modify the prediction route to handle new parameters
3. Retrain the model with additional features
4. Update the DataFrame columns in the prediction function

### Styling and UI
- Add CSS files to the `static/` folder
- Enhance the `index.html` template
- Implement responsive design for mobile compatibility

### Model Updates
- Replace `RidgeModel.pkl` with a newly trained model
- Ensure the new model expects the same input format
- Update preprocessing steps if needed

## 🐛 Troubleshooting

### Common Issues

1. **Missing Files Error**
   - Ensure `clean_data.csv` and `RidgeModel.pkl` are in the root directory
   - Check that `templates/index.html` exists

2. **Import Errors**
   - Verify all required packages are installed
   - Check Python version compatibility

3. **Prediction Errors**
   - Validate input data types and formats
   - Ensure the model was trained with compatible features

4. **Port Already in Use**
   - Change the port in `app.run(debug=True, port=5001)`
   - Or stop the existing Flask process

### Performance Optimization
- Implement caching for frequently used locations
- Add input validation on both frontend and backend
- Consider using a production WSGI server like Gunicorn

## 📊 Data Requirements

### Expected CSV Format (`clean_data.csv`)
The dataset should contain at least these columns:
- `location`: Property location/area names
- `total_sqft`: Property size in square feet
- `bhk`: Number of bedrooms
- `bath`: Number of bathrooms
- `price`: Target variable (for reference)

### Model Input Format
The trained model expects input in this exact order:
`['location', 'total_sqft', 'bhk', 'bath']`

## 🚀 Deployment

### Local Development
- Use `debug=True` for development
- Flask's built-in server is sufficient for testing

### Production Deployment
- Use a production WSGI server (Gunicorn, uWSGI)
- Set `debug=False` 
- Configure proper error handling and logging
- Consider containerization with Docker

Example production command:
```bash
gunicorn -w 4 -b 0.0.0.0:5000 app:app
```

## 📄 License

This project is open source. Ensure you have appropriate rights to use the real estate data according to your local regulations.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Implement your changes
4. Test thoroughly
5. Submit a pull request

## 📞 Support

For questions or issues:
- Check the troubleshooting section
- Review Flask documentation: https://flask.palletsprojects.com/
- Verify model and data file integrity

---

*Built with 🏠 using Flask, scikit-learn, and Python*
