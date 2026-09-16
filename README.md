```md
# MLOps Project - Vehicle Insurance Data Pipeline

Welcome to this MLOps learning project, designed to demonstrate the structure of an end-to-end machine learning pipeline for vehicle insurance data. The project includes data processing, model training, a FastAPI prediction application, Docker configuration, and a reference CI/CD workflow.

> **Project Status:** This is a student learning project. The local pipeline and application code are included for practice and development. AWS deployment and GitHub Actions CI/CD are included as implementation references, but they have **not been run** because I do not currently have access to an AWS account, ECR repository, EC2 instance, or required GitHub secrets.

---

## 📁 Project Setup and Structure

### Step 1: Project Template

- The `template.py` file can be used to create the initial project folder structure and placeholder files.

### Step 2: Package Management

- Local packages are configured through `setup.py` and `pyproject.toml`.
- **Tip:** See `crashcourse.txt` to learn more about package setup.

### Step 3: Virtual Environment and Dependencies

Create and activate a virtual environment, then install dependencies:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

Verify installed packages:

```powershell
pip list
```

---

## 📊 MongoDB Setup and Data Management

### Step 4: MongoDB Atlas Configuration

1. Create a project in [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).
2. Create a free M0 cluster.
3. Create a database user and add your IP address to Network Access.
4. Copy your MongoDB Python connection string.

### Step 5: Set the MongoDB Environment Variable

Set your MongoDB connection string before running training:

```powershell
$env:MONGODB_URL = "mongodb+srv://<username>:<password>@<cluster>/<database>"
```

> Do not upload your MongoDB password or connection string to GitHub.

### Step 6: Pushing Data to MongoDB

1. Use the dataset in the `notebook` folder.
2. Upload the vehicle insurance dataset to your MongoDB collection.
3. Confirm that the collection contains the data before running the training pipeline.

---

## 📝 Logging, Exception Handling, and EDA

### Step 7: Logging and Exception Handling

- Logging and custom exception handling are implemented in the `src/logger` and `src/exception` folders.
- The `demo.py` file can be used to run the training pipeline.

### Step 8: Exploratory Data Analysis and Feature Engineering

- EDA and dataset experimentation can be performed using the files in the `notebook` folder.
- The final pipeline uses processed vehicle insurance features for model training.

---

## 📥 Data Ingestion

### Step 9: Data Ingestion Pipeline

- MongoDB connection logic is available in `src/configuration/mongo_db_connection.py`.
- Data ingestion components are available in `src/components/data_ingestion.py`.
- Configuration and artifacts are managed through:
  - `src/entity/config_entity.py`
  - `src/entity/artifact_entity.py`

Run the training pipeline after setting `MONGODB_URL`:

```powershell
python demo.py
```

---

## 🔍 Data Validation, Transformation, and Model Training

### Step 10: Data Validation

- The data schema is defined in `config/schema.yaml`.
- Validation logic checks whether the ingested data matches the expected format.

### Step 11: Data Transformation

- Transformation logic is implemented in `src/components/data_transformation.py`.
- The preprocessing object and transformed data are saved as pipeline artifacts.

### Step 12: Model Training

- Model training is implemented in `src/components/model_trainer.py`.
- The project uses a Random Forest classifier for prediction.
- The model is evaluated before it is accepted for deployment.

---

## 🌐 AWS Setup for Model Evaluation and Deployment

> **Note:** AWS integration is included in this project as a learning reference. It has not been configured or executed because I do not currently have AWS access.

### Step 13: AWS and S3 Design

The project contains code for:

- AWS credential configuration
- Amazon S3 model storage
- Model push and pull operations
- Model registry design

Relevant files include:

- `src/configuration/aws_connection.py`
- `src/cloud_storage/aws_storage.py`
- `src/entity/s3_estimator.py`
- `src/components/model_pusher.py`

### Step 14: Model Evaluation and S3 Model Pusher

The intended workflow is:

```text
Model Training
    ↓
Model Evaluation
    ↓
Accepted Model
    ↓
Push Model to Amazon S3
    ↓
Load Model for Prediction
```

Because AWS credentials and the S3 bucket are not configured, the S3 model push and prediction workflow cannot be completed in the current version.

---

## 🚀 Prediction Pipeline and FastAPI Application

### Step 15: Prediction Pipeline

- Prediction logic is available in `src/pipline/prediction_pipeline.py`.
- The application accepts vehicle information through an HTML form.
- The trained model returns either:

```text
Response-Yes
```

or:

```text
Response-No
```

### Step 16: Run the FastAPI Application

Start the application:

```powershell
python app.py
```

Open this URL in your browser:

```text
http://localhost:5000
```

> **Current limitation:** Predictions require the trained model from Amazon S3. Without AWS credentials and an S3 model bucket, the prediction form may not return a result.

---

## 🐳 Docker Setup

### Step 17: Build the Docker Image

```powershell
docker build -t vehicle-insurance-mlops .
```

### Step 18: Run the Docker Container

```powershell
docker run --rm -p 5000:5000 vehicle-insurance-mlops
```

Open:

```text
http://localhost:5000
```

Docker packages the application, but it does not remove the current AWS S3 requirement for predictions.

---

## 🔄 CI/CD Setup with GitHub Actions and AWS

The workflow file `.github/workflows/aws.yaml` demonstrates the intended CI/CD design.

### Intended Workflow

```text
Push to main branch
    ↓
GitHub Actions builds Docker image
    ↓
Docker image is pushed to Amazon ECR
    ↓
EC2 self-hosted runner pulls the image
    ↓
Docker container runs on EC2
```

### Required GitHub Secrets

The AWS workflow requires these repository secrets:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_DEFAULT_REGION`
- `ECR_REPO`
- `MONGODB_URL`

### Current CI/CD Status

The CI/CD workflow is not active because the following resources are not available:

- AWS account
- IAM user credentials
- Amazon ECR repository
- Amazon EC2 instance
- GitHub Actions self-hosted runner
- GitHub repository secrets

The workflow remains in this repository to demonstrate my understanding of Docker-based CI/CD deployment using GitHub Actions, AWS ECR, and EC2.

---

## 🎯 Project Workflow Summary

1. **MongoDB Data Ingestion**
2. **Data Validation**
3. **Data Transformation**
4. **Model Training**
5. **Model Evaluation**
6. **Model Pushing to S3** *(planned — requires AWS)*
7. **FastAPI Prediction Application**
8. **Docker Containerisation**
9. **GitHub Actions CI/CD Design** *(not executed — requires AWS)*

---

## 🛠️ Future Improvements

- Add local model loading so predictions work without AWS.
- Add unit tests for pipeline components.
- Add a GitHub Actions CI workflow that runs tests without AWS credentials.
- Add model metrics and experiment tracking.
- Add data versioning.
- Configure AWS deployment when cloud resources become available.
- Use least-privilege IAM permissions instead of full administrator access.

---

## 📚 Additional Resources

- **Package setup:** See `crashcourse.txt`
- **Pipeline runner:** `demo.py`
- **FastAPI app:** `app.py`
- **Docker configuration:** `Dockerfile`
- **CI/CD workflow:** `.github/workflows/aws.yaml`

---

## 💬 Connect

If you found this project helpful or have any questions, feel free to connect with me.

Repository: [swati-mishra07/MLops-Proj1](https://github.com/swati-mishra07/MLops-Proj1)

---

This README documents my learning process while building an MLOps pipeline with MongoDB, FastAPI, Docker, AWS service integration design, and GitHub Actions CI/CD workflow design.
```