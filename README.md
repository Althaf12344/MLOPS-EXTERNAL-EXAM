# FDM 3D Printing Warping Defect Prediction using MLOps

## Project Overview

This project focuses on predicting warping defects in Fused Deposition Modeling (FDM) 3D printing using machine learning and MLOps practices.

Warping is a common defect in FDM printing. It occurs when different parts of a printed object cool unevenly, causing the material to contract and the edges of the object to lift from the build plate.

The objective of this project is to develop a machine learning system that analyzes printing parameters and predicts the possibility of warping defects.

The project also demonstrates an end-to-end MLOps workflow, including dataset versioning, data preprocessing, feature engineering, model training, experiment tracking, model registration, API deployment, and automated testing.

## Objectives

- Generate and manage datasets containing FDM printing parameters.
- Analyze the relationship between printing conditions and warping defects.
- Perform data preprocessing and feature engineering.
- Train and compare multiple machine learning models.
- Track experiments and register trained models using MLflow.
- Deploy the selected model using FastAPI.
- Implement automated testing and continuous integration using GitHub Actions.

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| Pandas | Data manipulation |
| NumPy | Numerical operations |
| Scikit-learn | Machine learning |
| Matplotlib | Data visualization |
| MLflow | Experiment tracking and model registry |
| FastAPI | Model deployment |
| Pydantic | Input validation |
| Pytest | Automated testing |
| Git & GitHub | Version control |
| GitHub Actions | Continuous integration |

## Dataset Description

Two synthetic datasets are used in this project.

| Dataset | Records | Description |
|---|---:|---|
| Printing Jobs V1 | 320 | Baseline printing conditions |
| Printing Jobs V2 | 320 | Modified conditions with higher printing speeds and generally lower bed temperatures |
| **Total** | **640** | |

### Dataset Features

The datasets contain the following parameters:

- Filament material (PLA, ABS, PETG)
- Nozzle temperature
- Bed temperature
- Printing speed
- Ambient temperature
- Cooling fan speed
- Component base area
- Layer height
- Nozzle-bed temperature difference
- Cooling stress index
- Warping defect (target variable)

The target variable is `warping_defect`:

- `0` – No warping defect
- `1` – Warping defect

**Note:** The datasets are synthetically generated for academic experimentation. They do not represent measurements collected from actual 3D printers.

## Project Workflow

1. **Dataset Generation:** Generate two datasets representing different FDM printing conditions.
2. **Data Preprocessing:** Handle missing values, encode categorical variables, and scale numerical features.
3. **Feature Engineering:** Calculate nozzle-bed temperature difference and cooling stress index.
4. **Model Training:** Train Logistic Regression and Random Forest classifiers.
5. **Model Evaluation:** Compare models using precision, recall, F1-score, and confusion matrices.
6. **Experiment Tracking:** Track model experiments and register the selected model using MLflow.
7. **Model Deployment:** Develop a REST API using FastAPI.
8. **Automated Testing:** Validate API endpoints and input parameters using Pytest.
9. **Continuous Integration:** Configure GitHub Actions to run automated tests.

## Machine Learning Models

The project implements two classification algorithms:

### 1. Logistic Regression
Used as a baseline classification model to predict whether a printing job is likely to produce a warping defect.

### 2. Random Forest Classifier
An ensemble learning algorithm that combines multiple decision trees to classify printing conditions.

The models are compared using classification evaluation metrics, and the selected model is registered in MLflow.

## Feature Engineering

Two additional features are generated:

**1. Nozzle-Bed Temperature Difference**

Calculates the temperature difference between the nozzle and the build plate.

**2. Cooling Stress Index**

An engineered feature that considers material type, thermal conditions, printing speed, fan speed, component geometry, and layer height.

These features help represent printing conditions that may influence warping risk.

## MLflow Experiment Tracking

MLflow is used to manage machine learning experiments.

The implementation includes:

- Experiment tracking
- Model parameter logging
- Model metric logging
- Model artifact storage
- Model registration

Registered model name:

`FDM_Warping_Predictor`

Registered model version:

`1`

## FastAPI Deployment

The trained model is deployed through a FastAPI application.

### Available Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Home endpoint |
| GET | `/health` | Check API and model status |
| POST | `/predict` | Generate a warping prediction |

### Example Prediction Input

```json
{
  "filament_material": "PLA",
  "nozzle_temperature_c": 210,
  "bed_temperature_c": 60,
  "printing_speed_mm_s": 50,
  "ambient_temperature_c": 23,
  "cooling_fan_speed_pct": 70,
  "component_base_area_mm2": 2500,
  "layer_height_mm": 0.2
}
```

The API validates the input parameters and returns a prediction along with the estimated warping probability.

## Automated Testing

Pytest is used to test the deployed API.

The test cases cover:

- Health endpoint response
- Home endpoint response
- Valid prediction request
- Invalid printing speed
- Invalid filament material
- Missing input parameters

The implemented test suite completed with **6 passed tests**.

GitHub Actions is configured to execute the automated tests during repository push and pull-request events.

## Project Structure

```text
3D_Print_Warping_MLOps/
│
├── data/
│   ├── raw/
│   │   ├── printing_jobs_v1.csv
│   │   └── printing_jobs_v2.csv
│   │
│   └── processed/
│       ├── feature_store_v1.csv
│       └── feature_store_v2.csv
│
├── models/
│   ├── warping_model.pkl
│   └── warping_model.joblib
│
├── reports/
│   ├── model_comparison.csv
│   ├── dataset_version_comparison.csv
│   └── figures/
│
├── .github/
│   └── workflows/
│       └── ci.yml
│
├── app.py
├── test_api.py
├── requirements.txt
├── .gitignore
└── README.md
```

## Installation and Execution

### 1. Clone the Repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
cd 3D_Print_Warping_MLOps
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the FastAPI Application

```bash
uvicorn app:app --host 0.0.0.0 --port 8000
```

### 4. Access API Documentation

Open the following URL in your browser:

```text
http://127.0.0.1:8000/docs
```

### 5. Run Automated Tests

```bash
pytest -v test_api.py
```

## Results

The implemented system achieved the following execution results:

- Generated two datasets containing 640 synthetic printing jobs in total.
- Implemented feature engineering and verified the generated features against the processed dataset.
- Trained Logistic Regression and Random Forest models.
- Registered the selected model in MLflow.
- Successfully tested FastAPI health and prediction endpoints.
- Verified input validation for invalid printing parameters.
- Executed six automated tests successfully.

## Future Enhancements

- Collect real-world FDM printing data.
- Integrate real-time sensor data from 3D printers.
- Explore advanced classification algorithms.
- Implement model monitoring and data drift detection.
- Develop a dashboard for visualizing printing conditions and predicted defects.
- Retrain models using newly collected printing data.

## Conclusion

This project demonstrates how machine learning and MLOps practices can be combined to develop a warping defect prediction system for FDM 3D printing. It covers the complete workflow, from dataset preparation and model development to experiment tracking, API deployment, and automated testing.

The system provides a foundation for further research into intelligent defect prediction and quality monitoring in additive manufacturing.
