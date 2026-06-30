Ames Housing – DVC Pipeline & MLflow Experiment Tracking
Author: Guangyuan Gao
Course: MLOps
Date: 2026‑06‑30

1. Project Overview
This repository implements a fully reproducible machine learning pipeline using:

DVC for data versioning and pipeline automation

MLflow for experiment tracking

CatBoost for model training

YAML configuration for parameter management

The pipeline trains a regression model on the Ames Housing dataset and evaluates its performance using RMSE and MAE.

All experiments are logged automatically to MLflow, and all artifacts are tracked by DVC.

2. Repository Structure
Code
mlopsproject/
│
├── data/
│   ├── raw/
│   │   └── ames.csv
│   └── processed/
│       ├── train.csv
│       └── test.csv
│
├── models/
│   └── catboost_model.cbm
│
├── reports/
│   └── metrics.json
│
├── src/
│   ├── prepare.py
│   ├── train.py
│   └── evaluate.py
│
├── params.yaml
├── dvc.yaml
├── dvc.lock
└── README.md
This structure follows standard MLOps conventions: clean separation of data, code, models, and configuration.

3. Installation & Setup
Clone the repository
Code
git clone <your-repo-url>
cd mlopsproject
Create environment
Code
conda create -n mlops python=3.10 -y
conda activate mlops
Install dependencies
Code
pip install -r requirements.txt
Initialize DVC
Code
dvc init
Start MLflow UI
Code
mlflow ui
Open in browser:

Code
http://127.0.0.1:5000
4. DVC Pipeline
The pipeline consists of three stages:

Stage 1 — prepare
Loads raw data

Drops ID column

Fills missing categorical values

Splits into train/test

Saves processed CSVs

Stage 2 — train
Loads processed training data

Detects categorical features

Trains CatBoost model

Logs parameters, metrics, and model artifact to MLflow

Saves model to models/catboost_model.cbm

Stage 3 — evaluate
Loads trained model

Predicts on test set

Computes RMSE and MAE

Saves metrics to reports/metrics.json

Run the full pipeline
Code
dvc repro
5. MLflow Experiment Tracking
Experiment: ames-catboost
Three runs were executed by modifying params.yaml:

Run 1 – Baseline
Code
depth: 6
learning_rate: 0.1
iterations: 300
Run 2 – Experiment 1
Code
depth: 8
learning_rate: 0.1
iterations: 300
Run 3 – Experiment 2
Code
depth: 6
learning_rate: 0.05
iterations: 500
Each run logs:

Parameters

RMSE

MAE

Model artifact

Screenshot: MLflow Experiment List
[Insert screenshot here]

Screenshot: MLflow Run Details
[Insert screenshot here]

6. Metrics Output
The evaluation stage produces:

Code
reports/metrics.json
Example:

json
{
  "rmse": 24567.12,
  "mae": 16789.44
}
These values change depending on the parameter settings in params.yaml.

7. Reproducibility
This project is fully reproducible because:

All data transformations are deterministic

All parameters are stored in params.yaml

All pipeline steps are defined in dvc.yaml

All artifacts are tracked in dvc.lock

All experiments are logged in MLflow

To reproduce any experiment:

Edit params.yaml

Run:

Code
dvc repro
View results in MLflow UI

8. Summary
This project demonstrates:

How to build a complete ML pipeline using DVC

How to track experiments with MLflow

How to manage parameters with YAML

How to train and evaluate a CatBoost model

How to maintain reproducibility across multiple runs

This README provides all documentation required for the assignment.
