# Jenkins CI/CD Pipeline for Flask Application

## Objective
Set up a Jenkins pipeline that automates the testing and deployment of a Python Flask web application.

## Repository
Project Repository:
https://github.com/shankarprasadtn/asset_QR_V1.2.3_final

## Application Overview
This project is a Flask-based Asset QR Management Application used to generate and manage QR-based asset records.

---

# Prerequisites

- Ubuntu / Linux VM
- Python 3.x
- pip
- Git
- Jenkins
- Internet connection

---

# Jenkins Setup

## Install Java
sudo apt update
sudo apt install openjdk-17-jdk -y

## Install Jenkins
sudo apt install jenkins -y

## Start Jenkins
sudo systemctl enable jenkins
sudo systemctl start jenkins

## Access Jenkins
http://localhost:8080

---

# Jenkins Pipeline Configuration

A `Jenkinsfile` was created in the root of the repository.

## Pipeline Stages

### 1. Checkout SCM
Jenkins clones the source code from GitHub.

### 2. Build
Installs all required Python dependencies from `requirements.txt`.

### 3. Test
Validates the Flask application using Python compile check.

### 4. Deploy
Runs the Flask application in the background.

### 5. Post Actions
Displays pipeline success or failure message.

---

# Jenkinsfile Used

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'python3 -m pip install --upgrade pip'
                sh 'pip3 install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'python3 -m py_compile app.py'
            }
        }

        stage('Deploy') {
            steps {
                sh 'nohup python3 app.py > app.log 2>&1 &'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}



````

#**Successful Execution**

The Jenkins pipeline executed successfully with all stages completed:

Checkout SCM
Build
Test
Deploy
Post Actions

**How to Run Application Manually**
pip install -r requirements.txt
python app.py

**Then open: http://localhost:5000**
