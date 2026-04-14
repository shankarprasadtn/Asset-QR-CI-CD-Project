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

## GitHub repo now contains: ##

* Flask app
* Jenkinsfile
* README.md
* Screenshots

1. <img width="959" height="557" alt="image" src="https://github.com/user-attachments/assets/b471b36d-7255-4418-be42-bd1d1aee7d1f" />
2. <img width="1919" height="1024" alt="Screenshot 2026-04-14 182709" src="https://github.com/user-attachments/assets/66043d26-e186-47af-8610-68318e93745f" />
3. <img width="1919" height="1049" alt="Screenshot 2026-04-14 182746" src="https://github.com/user-attachments/assets/5228fa98-6fdd-4071-a992-61ff44ab3862" />
4. <img width="1919" height="1117" alt="Screenshot 2026-04-14 182917" src="https://github.com/user-attachments/assets/8f22b1e3-b61e-410a-ab5f-f4d551d4bfb7" />
5. <img width="959" height="599" alt="image" src="https://github.com/user-attachments/assets/7ab6bc50-ee3a-4abe-8537-7c9de7ff3fa8" />
