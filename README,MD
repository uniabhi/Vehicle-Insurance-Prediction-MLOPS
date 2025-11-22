Vehicle Insurance Prediction - MLOps Project
📌 Project Overview
This project is an end-to-end Machine Learning application designed to predict vehicle insurance responses. It is built with a robust MLOps architecture, featuring a fully automated pipeline for data ingestion, validation, transformation, model training, and deployment. The application is served using FastAPI and is designed to be deployed on AWS using Docker and GitHub Actions for CI/CD.


🛠 Tech Stack

Language: Python 3.10 


Framework: FastAPI 


Database: MongoDB Atlas 

Machine Learning: Scikit-Learn, Pandas, NumPy


Containerization: Docker 



Cloud Provider: AWS (S3, ECR, EC2, IAM) 




CI/CD: GitHub Actions 

📂 Project Workflow
The project follows a modular pipeline structure:


Data Ingestion: Fetches data from MongoDB and splits it into train/test sets.


Data Validation: Validates data schema against schema.yaml.


Data Transformation: Handles feature engineering and preprocessing (saved as pickle objects).


Model Trainer: Trains the model and saves artifacts.


Model Evaluation: Compares the new model against the existing production model.



Model Pusher: Pushes the best model to the AWS S3 registry.



Prediction Pipeline: Serves predictions via a web interface.

⚙️ Installation & Setup
1. Clone the Repository
Bash

git clone <repository-url>
cd Vehicle-Insurance-Prediction-MLOPS
2. Environment Setup
Create and activate a Conda environment with Python 3.10.

Bash

conda create -n vehicle python=3.10 -y
conda activate vehicle
Install the required dependencies.

Bash

pip install -r requirements.txt
3. MongoDB Setup
Sign up for MongoDB Atlas and create a new project.

Create a M0 cluster and set up a database user.

Allow access from anywhere by adding IP 0.0.0.0/0 in "Network Access".

Get the connection string (Python driver) and save it.

4. Environment Variables
Export the following environment variables in your terminal or add them to your system environment:


Bash:

Bash

export MONGODB_URL="mongodb+srv://<username>:<password>..."
export AWS_ACCESS_KEY_ID="<YOUR_AWS_ACCESS_KEY>"
export AWS_SECRET_ACCESS_KEY="<YOUR_AWS_SECRET_KEY>"
export AWS_DEFAULT_REGION="us-east-1"
PowerShell:

PowerShell

$env:MONGODB_URL = "mongodb+srv://<username>:<password>..."
$env:AWS_ACCESS_KEY_ID = "<YOUR_AWS_ACCESS_KEY>"
$env:AWS_SECRET_ACCESS_KEY = "<YOUR_AWS_SECRET_KEY>"
$env:AWS_DEFAULT_REGION = "us-east-1"
🚀 Usage
Running Locally
Start the FastAPI application:

Bash

python app.py

Web Interface: Open http://localhost:5080 (or the port specified in constants) to access the form.


Train Model: Navigate to /train endpoint to trigger the training pipeline.

Docker
Build and run the Docker container locally:

Bash

docker build -t vehicle-app .
docker run -p 5080:5080 vehicle-app
☁️ Deployment (AWS & CI/CD)
1. AWS Configuration

IAM User: Create a user (firstproj) with AdministratorAccess and generate CLI access keys.


S3 Bucket: Create a bucket named my-model-mlopsproj in us-east-1 for model artifacts.


ECR Repository: Create a repository named vehicleproj to store Docker images.


EC2 Instance: Launch an Ubuntu Server 24.04 (T2 Medium) instance. Configure security groups to allow HTTP/HTTPS and Custom TCP on port 5080.


2. GitHub Actions (CI/CD)
Self-Hosted Runner: * Go to GitHub Settings > Actions > Runners > New self-hosted runner.

Run the provided commands on your EC2 instance to configure the runner.

Secrets: Add the following secrets to your GitHub Repository:

AWS_ACCESS_KEY_ID

AWS_SECRET_ACCESS_KEY

AWS_DEFAULT_REGION


ECR_REPO 

3. Trigger Deployment
Pushing a new commit to the main branch will trigger the GitHub Actions workflow, which builds the Docker image, pushes it to AWS ECR, and deploys it to your EC2 instance.

👤 Author

Abhishek Kumar Email: abhishek074.kr@gmail.com