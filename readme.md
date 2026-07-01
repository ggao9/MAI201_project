# House Price Prediction

An end-to-end Machine Learning Operations (MLOps) pipeline for predicting residential property prices using the Ames Housing dataset. This project demonstrates reproducible data versioning, experiment tracking, automated model training, and evaluation using industry-standard MLOps tools.

---

## Overview

This repository implements a production-oriented machine learning workflow that emphasizes reproducibility, automation, and experiment management.

The pipeline includes:

- Data preparation
- Feature preprocessing
- Model training
- Model evaluation
- Experiment tracking with MLflow
- Data and model versioning with DVC
- Configuration-driven experimentation

The objective is to build a repeatable workflow where datasets, model artifacts, metrics, and experiments remain fully reproducible throughout the machine learning lifecycle.

---

## Architecture

<p align="center">
  <img src="images/pipeline-diagram.png" width="900" alt="Pipeline Architecture">
</p>

The pipeline follows the workflow below:

```text
                Raw Dataset
                     │
                     ▼
            Data Preparation
                     │
                     ▼
          Feature Engineering
                     │
                     ▼
          Model Training
             (CatBoost)
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
    Model Artifact         Evaluation
          │                     │
          └──────────┬──────────┘
                     ▼
        DVC + MLflow Tracking
```

---

## Repository Structure

```text
house-price-prediction/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── images/
│
├── models/
│
├── reports/
│
├── src/
│   ├── prepare.py
│   ├── train.py
│   └── evaluate.py
│
├── params.yaml
├── dvc.yaml
├── dvc.lock
├── requirements.txt
└── README.md
```

---

## Technology Stack

| Component | Technology |
|-----------|------------|
| Language | Python |
| Model | CatBoost |
| Experiment Tracking | MLflow |
| Data Versioning | DVC |
| Configuration | YAML |
| Version Control | Git |

---

## Dataset

**Dataset**

House Prices: Advanced Regression Techniques

**Source**

https://www.kaggle.com/c/house-prices-advanced-regression-techniques

**Target Variable**

```
SalePrice
```

The dataset contains numerical and categorical attributes describing residential properties in Ames, Iowa. The objective is to predict the final sale price of each property.

---

## Pipeline

The pipeline consists of three reproducible stages.

### Data Preparation

- Load raw dataset
- Clean missing values
- Split train and test datasets
- Save processed data

### Model Training

- Read hyperparameters from `params.yaml`
- Train CatBoost model
- Save trained model
- Log experiment metadata

### Evaluation

- Generate predictions
- Calculate evaluation metrics
- Store metrics
- Log results to MLflow

---

## Running the Pipeline

Clone the repository.

```bash
git clone https://github.com/yourusername/house-price-prediction.git

cd house-price-prediction
```

Install dependencies.

```bash
pip install -r requirements.txt
```

Run the complete pipeline.

```bash
dvc repro
```

Launch MLflow.

```bash
mlflow ui
```

---

## Configuration

Pipeline parameters are managed through

```text
params.yaml
```

This enables reproducible experimentation without modifying application code.

---

## Experiment Tracking

MLflow is used to record

- Parameters
- Metrics
- Model artifacts
- Experiment history

Each pipeline execution produces a fully traceable experiment for comparison and reproducibility.

---

## Data Versioning

DVC manages

- Raw datasets
- Processed datasets
- Trained models
- Evaluation reports

Versioning data independently of Git ensures reproducible machine learning experiments while keeping the repository lightweight.

---

## Model

The project uses **CatBoost Regressor**, which provides:

- Native support for categorical features
- Minimal preprocessing requirements
- Strong regression performance
- Efficient handling of missing values
- Reduced overfitting through ordered boosting

---

## Evaluation

The model is evaluated using standard regression metrics.

- RMSE
- MAE
- R² Score

Evaluation reports are stored in

```text
reports/metrics.json
```

---

## Future Work

Planned improvements include

- CI/CD with GitHub Actions
- Docker support
- FastAPI model serving
- Model registry
- Drift detection
- Automated retraining
- Cloud deployment
- Monitoring and alerting

---

## License

This project is licensed under the MIT License.

---

## **Prepared by:** 

Gao-Ali-Suhayel
