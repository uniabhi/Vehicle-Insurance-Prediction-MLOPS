# Vehicle Insurance Prediction - MLOps Project

![Python](https://img.shields.io/badge/Python-3.10-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-green)
![Docker](https://img.shields.io/badge/Docker-Enabled-blue)
![AWS](https://img.shields.io/badge/AWS-S3%20|%20ECR%20|%20EC2-orange)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-green)

## 📌 Project Overview

This project is an end-to-end Machine Learning application designed to predict vehicle insurance responses. It is built with a robust MLOps architecture, featuring a fully automated pipeline for data ingestion, validation, transformation, model training, and deployment. The application is served using FastAPI and is designed to be deployed on AWS using Docker and GitHub Actions for CI/CD.

---

## 🛠 Tech Stack

| Category | Technology |
|----------|------------|
| **Language** | Python 3.10 |
| **Framework** | FastAPI |
| **Database** | MongoDB Atlas |
| **ML Libraries** | Scikit-Learn, Pandas, NumPy |
| **Containerization** | Docker |
| **Cloud Provider** | AWS (S3, ECR, EC2, IAM) |
| **CI/CD** | GitHub Actions |

---

## 📂 Project Workflow

The project follows a modular pipeline structure:

```
Data Ingestion → Data Validation → Data Transformation → Model Trainer → Model Evaluation → Model Pusher → Prediction Pipeline
```

| Step | Description |
|------|-------------|
| **1. Data Ingestion** | Fetches data from MongoDB and splits it into train/test sets |
| **2. Data Validation** | Validates data schema against `schema.yaml` |
| **3. Data Transformation** | Handles feature engineering and preprocessing (saved as pickle objects) |
| **4. Model Trainer** | Trains the model and saves artifacts |
| **5. Model Evaluation** | Compares the new model against the existing production model |
| **6. Model Pusher** | Pushes the best model to the AWS S3 registry |
| **7. Prediction Pipeline** | Serves predictions via a web interface |

---

## ⚙️ Installation & Setup

### 1. Clone the Repository

```bash
git clone <repository-url>
cd Vehicle-Insurance-Prediction-MLOPS
```

### 2. Environment Setup

Create and activate a Conda environment with Python 3.10:

```bash
conda create -n vehicle python=3.10 -y
conda activate vehicle
```

Install the required dependencies:

```bash
pip install -r requirements.txt
```

### 3. MongoDB Setup

1. Sign up for [MongoDB Atlas](https://www.mongodb.com/atlas) and create a new project
2. Create a **M0 cluster** and set up a database user
3. Allow access from anywhere by adding IP `0.0.0.0/0` in **Network Access**
4. Get the connection string (Python driver) and save it

### 4. Environment Variables

#### For Bash/Linux/macOS:

```bash
export MONGODB_URL="mongodb+srv://<username>:<password>@cluster..."
export AWS_ACCESS_KEY_ID="<YOUR_AWS_ACCESS_KEY>"
export AWS_SECRET_ACCESS_KEY="<YOUR_AWS_SECRET_KEY>"
export AWS_DEFAULT_REGION="us-east-1"
```

#### For PowerShell/Windows:

```powershell
$env:MONGODB_URL = "mongodb+srv://<username>:<password>@cluster..."
$env:AWS_ACCESS_KEY_ID = "<YOUR_AWS_ACCESS_KEY>"
$env:AWS_SECRET_ACCESS_KEY = "<YOUR_AWS_SECRET_KEY>"
$env:AWS_DEFAULT_REGION = "us-east-1"
```

---

## 🚀 Usage

### Running Locally

Start the FastAPI application:

```bash
python app.py
```

| Endpoint | Description |
|----------|-------------|
| `http://localhost:5080` | Web Interface - Access the prediction form |
| `http://localhost:5080/train` | Training Endpoint - Trigger the training pipeline |

### Docker

Build and run the Docker container locally:

```bash
# Build the image
docker build -t vehicle-app .

# Run the container
docker run -p 5080:5080 vehicle-app
```

---

## ☁️ Deployment (AWS & CI/CD)

### 1. AWS Configuration

| Service | Configuration |
|---------|---------------|
| **IAM User** | Create a user (`firstproj`) with `AdministratorAccess` and generate CLI access keys |
| **S3 Bucket** | Create bucket named `my-model-mlopsproj` in `us-east-1` for model artifacts |
| **ECR Repository** | Create repository named `vehicleproj` to store Docker images |
| **EC2 Instance** | Launch Ubuntu Server 24.04 (T2 Medium) with security groups allowing HTTP/HTTPS and Custom TCP on port 5080 |

### 2. GitHub Actions (CI/CD)

#### Self-Hosted Runner Setup:

1. Go to **GitHub Settings** → **Actions** → **Runners** → **New self-hosted runner**
2. Run the provided commands on your EC2 instance to configure the runner

#### GitHub Secrets:

Add the following secrets to your GitHub Repository (**Settings** → **Secrets and variables** → **Actions**):

| Secret Name | Description |
|-------------|-------------|
| `AWS_ACCESS_KEY_ID` | Your AWS access key |
| `AWS_SECRET_ACCESS_KEY` | Your AWS secret key |
| `AWS_DEFAULT_REGION` | AWS region (e.g., `us-east-1`) |
| `ECR_REPO` | ECR repository URI |

### 3. Trigger Deployment

Pushing a new commit to the `main` branch will trigger the GitHub Actions workflow, which:

1. ✅ Builds the Docker image
2. ✅ Pushes it to AWS ECR
3. ✅ Deploys it to your EC2 instance

---

## 📁 Project Structure

```
Vehicle-Insurance-Prediction-MLOPS/
│
├── src/
│   ├── components/
│   │   ├── data_ingestion.py
│   │   ├── data_validation.py
│   │   ├── data_transformation.py
│   │   ├── model_trainer.py
│   │   ├── model_evaluation.py
│   │   └── model_pusher.py
│   ├── pipeline/
│   │   ├── training_pipeline.py
│   │   └── prediction_pipeline.py
│   ├── utils/
│   └── config/
│
├── templates/
├── static/
├── artifacts/
├── app.py
├── requirements.txt
├── Dockerfile
├── schema.yaml
├── projectflow.txt
└── README.md
```

---

## 👤 Author

**Abhishek Kumar**

📧 Email: abhishek074.kr@gmail.com

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 📚 Additional Resources

For more details on the project flow, refer to `projectflow.txt` included in the repository.