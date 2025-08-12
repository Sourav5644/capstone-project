# 🎬 IMDB Review Sentiment Analysis

## 📌 Project Overview
This project performs **sentiment analysis** on IMDB movie reviews using a complete **MLOps pipeline**.  
It covers everything from **data ingestion** to **model deployment** on AWS, with experiment tracking, version control, CI/CD automation.

---

## 🚀 Features
- **Data Pipeline**: Built using `DVC` for versioning datasets & ML pipelines.
- **Experiment Tracking**: Managed via `MLflow` on DagsHub.
- **Model Training**: Sentiment classification using IMDb dataset.
- **CI/CD**: GitHub Actions pipeline for automation.
- **Containerization**: Dockerized Flask API for model inference.
- **Cloud Deployment**: AWS with LoadBalancer service.

---

## 🛠️ Tech Stack
- **Language**: Python 3.10
- **Frameworks**: Flask, scikit-learn
- **Tools**: DVC, MLflow, Cookiecutter, GitHub Actions
- **Cloud**: AWS EKS, ECR, S3
- **Container**: Docker

---

## 📂 Project Structure
├── src/
│ ├── logger.py
│ ├── data_ingestion.py
│ ├── data_preprocessing.py
│ ├── feature_engineering.py
│ ├── model_building.py
│ ├── model_evaluation.py
│ ├── register_model.py
│
├── flask_app/
│ ├── app.py
│ ├── templates/
│ ├── static/
│
├── tests/
├── scripts/
├── dvc.yaml
├── params.yaml
├── requirements.txt
├── Dockerfile
├── .github/workflows/ci.yaml
└── README.md


---

## ⚙️ Setup Instructions

### 1️⃣ Environment Setup
```bash
# Clone repo
git clone <repo-url>
cd <repo-name>

# Create & activate environment
conda create -n atlas python=3.10
conda activate atlas

# Install dependencies
pip install cookiecutter dagshub mlflow dvc flask

2️⃣ Cookiecutter Project Structure
```bash
cookiecutter -c v1 https://github.com/drivendata/cookiecutter-data-science
mv src.models src.model
git add .
git commit -m "Initial project structure"
git push

3️⃣ MLflow Setup with DagsHub
Create a new repo on DagsHub and connect it to GitHub.

Copy the experiment tracking URL & update in your scripts.

Test MLflow UI via browser.

4️⃣ DVC Pipeline
```bash
dvc init
mkdir local_s3
dvc remote add -d mylocal local_s3
# Add stages in dvc.yaml up to model evaluation
dvc repro
dvc status
git add .
git commit -m "DVC pipeline setup"
git push

5️⃣ AWS S3 Remote for DVC
```bash
pip install "dvc[s3]" awscli
aws configure
dvc remote add -d myremote s3://<bucket-name>

6️⃣ Flask API
```bash
cd flask_app
pip install flask
python app.py

7️⃣ Dockerization
```bash
pip install pipreqs
cd flask_app && pipreqs . --force
docker build -t capstone-app:latest .
docker run -p 8888:5000 -e CAPSTONE_TEST=<token> capstone-app:latest

