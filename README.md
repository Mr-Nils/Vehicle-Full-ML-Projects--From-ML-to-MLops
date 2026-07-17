# 🚗 Vehicle Insurance MLOps End-to-End Pipeline

[![Python](https://img.shields.io/badge/Python-3.10-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![AWS](https://img.shields.io/badge/AWS-S3_%7C_ECR_%7C_EC2-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/)
[![Docker](https://img.shields.io/badge/Docker-Container-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI%2FCD-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)](https://github.com/features/actions)

Welcome to the **Vehicle Insurance Data Pipeline** project! This repository demonstrates an enterprise-grade, end-to-end Machine Learning Operations (MLOps) pipeline designed for real-world vehicle insurance data management, model training, evaluation, and automated cloud deployment.

---

## 🎯 Project Workflow

┌─────────────────┐     ┌──────────────────┐     ┌─────────────────────┐
│  Data Ingestion ├────►│  Data Validation ├────►│ Data Transformation │
└─────────────────┘     └──────────────────┘     └──────────┬──────────┘
│
┌─────────────────┐     ┌──────────────────┐     ┌──────────▼──────────┐
│ Model Deployment│◄────┤ Model Evaluation │◄────┤    Model Training   │
└────────┬────────┘     └──────────────────┘     └─────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────────────────┐
│       Automated CI/CD (GitHub Actions ➔ Docker ➔ AWS ECR / EC2)       │
└──────────────────────────────────────────────────────────────────────┘


---

## 📁 1. Project Setup and Structure

### Step 1: Initialize Project Template
Generate the standard project folder structure and boilerplate placeholders:
```bash
python template.py
Step 2: Package Management Configuration
Configure package builds using setup.py and pyproject.toml to allow local module imports (src directory).

(Refer to crashcourse.txt for details on setuptools packaging).

Step 3: Virtual Environment Setup
Create a dedicated Conda environment and install dependencies:

Bash
# Create and activate environment
conda create -n vehicle python=3.10 -y
conda activate vehicle

# Install requirements
pip install -r requirements.txt

# Verify local package installation
pip list
📊 2. Database Management (MongoDB Atlas)
Step 4: MongoDB Atlas Setup
Log in to MongoDB Atlas and create a new project.

Spin up a free-tier M0 Cluster.

Create database user credentials (username/password).

Allow network access from anywhere (0.0.0.0/0).

Copy the Python connection string for later environment configuration.

Step 5: Data Ingestion to MongoDB
Store raw datasets inside the notebook/ directory.

Execute notebook/mongoDB_demo.ipynb to seed the database.

Validate uploaded collections via Database > Browse Collections in Atlas.

📝 3. Core Engine (Logging, Exception Handling, EDA)
Step 6: Logging & Custom Exception Modules
Built-in customized logging and exception handling modules catch real-time errors across pipeline components.

Test robustness: python demo.py

Step 7: Exploratory Data Analysis & Feature Engineering
Open and run notebook/EDA_and_Feature_Engg.ipynb to perform correlation analysis, outlier treatment, and feature selection before embedding transformation logic into production modules.

📥 4. Pipeline Components
Step 8: Data Ingestion
MongoDB Connector: Managed in configuration/mongo_db_connections.py.

Ingestion Logic: Handles database fetching and initial split inside data_access/ and components/data_ingestion.py.

Config Entities: Updated entity/config_entity.py and entity/artifact_entity.py.

Important: Export your database environment variables before running the ingestion pipeline:

Linux / macOS (Bash):

Bash
export MONGODB_URL="mongodb+srv://<username>:<password>@cluster.mongodb.net/..."
Windows (PowerShell):

PowerShell
$env:MONGODB_URL = "mongodb+srv://<username>:<password>@cluster.mongodb.net/..."
Step 9: Data Validation
Define structural expectations and column schema inside config/schema.yaml.

Execute runtime validation checks via utils/main_utils.py.

Step 10: Data Transformation
Implement preprocessing transformers, imputers, and scalers in components/data_transformation.py.

Build target estimators in entity/estimator.py.

Step 11: Model Training
Execute model training algorithms, hyperparameter tuning, and cross-validation inside components/model_trainer.py.

🌐 5. AWS Cloud Setup & Model Registry
Step 12: AWS Credentials & Permissions
Create an IAM user in the AWS Management Console with AdministratorAccess.

Export your credentials:

Bash
export AWS_ACCESS_KEY_ID="YOUR_AWS_ACCESS_KEY_ID"
export AWS_SECRET_ACCESS_KEY="YOUR_AWS_SECRET_ACCESS_KEY"
Update key bindings in constants/__init__.py.

Step 13: S3 Bucket & Artifact Storage
Create an S3 bucket named my-model-mlopsproj in us-east-1.

Manage cloud model pushes/pulls using src/aws_storage and entity/s3_estimator.py.

🚀 6. Evaluation, Prediction API, and Web UI
Step 14 & 15: Evaluation, Model Pusher & Web Application
Evaluate candidates against baseline production models. If performance metrics are met, push the model to S3.

Expose real-time prediction endpoints with app.py.

Web UI templates and static assets are located in /templates and /static.

🔄 7. CI/CD Deployment Architecture (Docker, ECR, EC2)
┌──────────────┐      ┌─────────────────┐      ┌──────────────┐      ┌─────────────┐
│ Git Push /   ├─────►│ GitHub Actions  ├─────►│   Amazon     ├─────►│  Amazon     │
│ Main Branch  │      │ Runner Pipeline │      │     ECR      │      │ EC2 Instance│
└──────────────┘      └─────────────────┘      └──────────────┘      └─────────────┘
Step 16: Containerization & CI Configuration
Configure container instructions inside Dockerfile and .dockerignore.

Navigate to GitHub Repository Settings > Secrets and variables > Actions and add:

AWS_ACCESS_KEY_ID

AWS_SECRET_ACCESS_KEY

AWS_DEFAULT_REGION

ECR_REPO

Step 17: AWS EC2 & ECR Provisioning
Provision an AWS EC2 instance (Ubuntu recommended).

Install Docker engine on the server.

Configure the EC2 instance as a Self-Hosted Runner in GitHub Repository Settings.

Step 18: Live Deployment
Update inbound Security Group rules on AWS to open Port 5080.

Run the deployment pipeline and access the web app:

http://<YOUR_EC2_PUBLIC_IP>:5080
🛠️ Additional Resources
crashcourse.txt: Architectural breakdown of Python setuptools, editable installs (-e .), setup.py, and pyproject.toml.

GitHub Secrets Guide: Best practices on managing secure IAM deployment credentials for CI/CD pipelines.

💬 Connect & Support
If you found this MLOps pipeline blueprint helpful, please consider starring ⭐ this repository! Feel free to reach out with feedback or questions.
