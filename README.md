# Vehicle Insurance MLOps Pipeline

<p align="center">
  An end-to-end machine learning project for predicting customer interest in vehicle insurance.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white" alt="FastAPI">
  <img src="https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/MongoDB-47A248?logo=mongodb&logoColor=white" alt="MongoDB">
  <img src="https://img.shields.io/badge/Status-Learning%20Project-8B5CF6" alt="Status">
</p>

## Overview

This project demonstrates the structure of an end-to-end MLOps pipeline using vehicle insurance data. It covers data ingestion, validation, transformation, model training, model evaluation, prediction serving with FastAPI, and Docker containerisation.

> **Project status:** This is a learning project. AWS deployment and GitHub Actions CI/CD are included as reference implementations, but they have not been executed because AWS resources, EC2 infrastructure, ECR, and repository secrets are not currently configured.

## Features

- MongoDB Atlas data ingestion
- Data validation using YAML schema
- Data transformation and preprocessing
- Random Forest model training and evaluation
- FastAPI web application for predictions
- Docker configuration for containerisation
- AWS S3 model registry design
- GitHub Actions CI/CD workflow reference

## Workflow

```text
MongoDB Atlas
    ↓
Data Ingestion
    ↓
Data Validation
    ↓
Data Transformation
    ↓
Model Training
    ↓
Model Evaluation
    ↓
Amazon S3 Model Registry (requires AWS)
    ↓
FastAPI Prediction Application
```

## Project Structure

```text
.
├── app.py
├── config/
│   ├── model.yaml
│   └── schema.yaml
├── notebook/
├── src/
│   ├── components/
│   ├── configuration/
│   ├── cloud_storage/
│   ├── entity/
│   ├── exception/
│   ├── logger/
│   └── pipline/
├── static/
├── templates/
├── Dockerfile
├── requirements.txt
└── .github/workflows/aws.yaml
```

## Local Setup

### Clone the repository

```powershell
git clone https://github.com/swati-mishra07/MLops-Proj1.git
cd MLops-Proj1
```

### Create a virtual environment

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

### Install dependencies

```powershell
pip install -r requirements.txt
```

### Configure MongoDB

Set your MongoDB Atlas connection string before running the training pipeline:

```powershell
$env:MONGODB_URL = "mongodb+srv://<username>:<password>@<cluster>/<database>"
```

> Never upload your MongoDB connection string or passwords to GitHub.

## Train the Model

Run the training pipeline:

```powershell
python demo.py
```

The pipeline performs data ingestion, validation, transformation, model training, and evaluation.

## Run the FastAPI Application

```powershell
python app.py
```

Open the application in your browser:

```text
http://localhost:5000
```

## Docker

Build the Docker image:

```powershell
docker build -t vehicle-insurance-mlops .
```

Run the container:

```powershell
docker run --rm -p 5000:5000 vehicle-insurance-mlops
```

Then visit:

```text
http://localhost:5000
```

## AWS and CI/CD Design

The repository includes an AWS deployment workflow in:

```text
.github/workflows/aws.yaml
```

The intended workflow is:

```text
Push to main branch
    ↓
GitHub Actions builds Docker image
    ↓
Push image to Amazon ECR
    ↓
EC2 self-hosted runner pulls and runs the container
```

The workflow requires these GitHub Secrets:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_DEFAULT_REGION`
- `ECR_REPO`
- `MONGODB_URL`

## Current Limitations

- AWS deployment has not been executed.
- Amazon S3 model storage requires AWS credentials.
- Predictions may fail if the S3 model bucket is unavailable.
- A local model-loading fallback is planned for future development.

## Future Improvements

- [ ] Add local model loading without AWS.
- [ ] Add unit tests for ML pipeline components.
- [ ] Add a CI workflow for testing without cloud credentials.
- [ ] Add model performance tracking.
- [ ] Add experiment tracking and data versioning.
- [ ] Deploy the application when AWS resources are available.

## Learning Outcomes

This project helped me practise:

- Building an MLOps pipeline
- Working with MongoDB Atlas
- Training and evaluating machine learning models
- Serving predictions using FastAPI
- Containerising applications with Docker
- Designing AWS-based CI/CD workflows with GitHub Actions

## Repository

[GitHub Repository](https://github.com/swati-mishra07/MLops-Proj1)
```