# Employee Attrition Prediction - AI Coding Guidelines

## Project Overview
This is a Flask-based web application for predicting employee attrition using a Logistic Regression model trained on IBM HR Analytics data. The app takes employee features via a web form and outputs attrition risk.

## Architecture
- **Web Layer**: Flask app (`app.py`) handles routing, form processing, and result rendering using Jinja2 templates (`templates/index.html`).
- **Model Layer**: Pre-trained Logistic Regression model (`model.pkl`) loaded via pickle for predictions.
- **Data Flow**: User inputs → Feature engineering in `app.py` → Model prediction → HTML response.

## Key Components
- `app.py`: Main Flask application with `/` (home) and `/predict` (POST) routes. Implements identical preprocessing to `model.py`.
- `model.py`: Data preprocessing and model training script (run once to generate `model.pkl`).
- `Attrition.ipynb`: Jupyter notebook for exploratory data analysis and model comparison.
- `datasets/WA_Fn-UseC_-HR-Employee-Attrition.csv`: Training dataset.
- `templates/index.html`: Web form with inputs for all 35 features.
- `static/`: Bootstrap CSS/JS for styling.

## Data Preprocessing Patterns
- **Feature Engineering**: Convert continuous features to boolean flags based on EDA thresholds (e.g., `Age_bool = 1 if Age < 35 else 0` in `app.py` lines 78-80).
- **Categorical Encoding**: Manual one-hot encoding for variables like BusinessTravel, Education (see `app.py` lines 151-200).
- **Derived Features**: `Total_Satisfaction` as average of satisfaction metrics, then binarized (lines 71-76).
- Always maintain identical preprocessing between training (`model.py`) and inference (`app.py`).

## Development Workflow
- **Setup**: `pip install -r requirements.txt` (Python 3.7+).
- **Run Locally**: `python app.py` or `flask run` (ensure `model.pkl` exists).
- **Train Model**: Execute `model.py` to regenerate `model.pkl` after data changes.
- **EDA**: Use `Attrition.ipynb` for analysis; export insights to update preprocessing.
- **Debug**: Check form inputs match dataset schema; verify preprocessing outputs match training features.

## Deployment
- **Heroku**: Uses `Procfile` (`web: gunicorn app:app`) and `runtime.txt` (Python 3.7.0).
- **Dependencies**: Listed in `requirements.txt`; includes Flask, scikit-learn, pandas.

## Conventions
- Preprocessing logic duplicated between `model.py` and `app.py` - keep synchronized.
- Boolean features named with `_bool` suffix (e.g., `Age_bool`).
- Categorical dummies prefixed with original name (e.g., `BusinessTravel_Rarely`).
- No automated testing; validate manually via web interface.

## Common Patterns
- When adding features: Update both `model.py` (training) and `app.py` (inference) preprocessing.
- Form validation: HTML inputs have min/max constraints matching dataset ranges.
- Model updates: Retrain on full dataset, save new `model.pkl`, redeploy.</content>
<parameter name="filePath">c:\Users\mahak\Downloads\Employee-Attrition-Prediction-code\Employee-Attrition-Prediction-code\.github\copilot-instructions.md