Here's a clean and professional `README.md` file based on the `NETFLIX.docx` content for your GitHub repository:

---

````markdown
# 🎬 Netflix Clone CI/CD Deployment with Jenkins & Apache Tomcat on AWS

This project demonstrates how to build a complete **CI/CD pipeline** using **Jenkins** and **Apache Tomcat** on **AWS EC2** instances to automate the deployment of a Netflix clone Java web application. This setup leverages DevOps best practices for continuous integration and delivery.

---

## 🔧 Technologies Used

- **Jenkins** (CI/CD automation)
- **Apache Tomcat 9** (Application Server)
- **AWS EC2** (Infrastructure hosting)
- **Maven** (Build tool)
- **Git & GitHub** (Version control)
- **Java 17 (Amazon Corretto)**

---

## 📌 Project Overview

- Jenkins installed on one EC2 instance.
- Two EC2 instances configured with Apache Tomcat.
- WAR file deployment managed via Jenkins pipeline.
- Source code fetched from GitHub.
- Fully automated build-test-deploy cycle.

---

## 🛠️ Setup Instructions

### 1️⃣ Jenkins Setup

- Launch an EC2 instance (Amazon Linux 2, t2.micro)
- Open ports: 22, 8080, 80, 50000
- Connect via SSH and run:

```bash
sudo -i
# Download and run setup script
curl -O https://raw.githubusercontent.com/confideoit/Confideo-All_Setup/main/jenkins.sh
bash jenkins.sh
````

* Start Jenkins and open in browser:

```
http://<jenkins-public-ip>:8080
```

* Get the admin password:

```bash
cat /var/lib/jenkins/secrets/initialAdminPassword
```

---

### 2️⃣ Tomcat Setup on Two Instances

* Launch 2 EC2 instances (Amazon Linux 2, t2.micro)
* Connect and run:

```bash
sudo -i
yum install git java-17-amazon-corretto -y
curl -O https://raw.githubusercontent.com/confideoit/Confideo-All_Setup/main/tomcat.sh
bash tomcat.sh
```

* Open in browser:

```
http://<tomcat-instance-public-ip>:8080/manager/html
```

> Username: `tomcat` | Password: `confideo123`

---

### 3️⃣ Jenkins Configuration

* Go to **Manage Jenkins → Nodes → New Node**
* Add both Tomcat instances as permanent agents
* Use **private IP** in the "Host" field

---

### 4️⃣ Credentials & Plugins

* Go to **Manage Jenkins → Credentials → Global → Add Credentials**

  * Use Tomcat username and password
* Go to **Manage Jenkins → Plugins**

  * Install: `Deploy to container` and `Pipeline Stage View`

---

## 🧪 Jenkins Pipeline Configuration

1. Create a new Pipeline job
2. Use the following script in **Pipeline → Script** section:

```groovy
pipeline {
    agent any

    stages {
        stage('code') {
            steps {
                git branch: 'main', url: 'https://github.com/confideoit/Confideo-Netflix-Jenkins-ec2.git'
            }
        }
        stage('build') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('sonarqube') {
            steps {
                echo "my code is tested"
            }
        }
        stage('artifact') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('nexus') {
            steps {
                echo "my artifact is stored on nexus"
            }
        }
        stage('deploy') {
            steps {
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'YOUR_CREDENTIAL_ID',
                        path: '',
                        url: 'http://<tomcat-public-ip>:8080/'
                    )
                ],
                contextPath: 'netflix',
                war: 'target/NETFLIX-1.2.2.war'
            }
        }
    }

    post {
        always {
            echo "my code deployed"
        }
    }
}
```

---

## 🛠 Replace in Script

* Replace the GitHub URL with your own repo if needed:

  ```groovy
  git url: 'https://github.com/YOUR_USERNAME/YOUR_REPO.git'
  ```
* Update `credentialsId` with your generated Jenkins credential ID
* Change Tomcat `url` to your own EC2 public IP

---

## 📥 Clone / Fork Repositories

* Jenkins Project Repo:
  [https://github.com/confideoit/Confideo-Netflix-Jenkins-ec2.git](https://github.com/confideoit/Confideo-Netflix-Jenkins-ec2.git)

* Jenkins & Tomcat Setup Scripts:
  [https://github.com/confideoit/Confideo-All\_Setup](https://github.com/confideoit/Confideo-All_Setup)

---

## 🧪 Trigger the Build

* Go to Jenkins Dashboard → Your Project → Click on **Build Now**
* Check the console output for stage-by-stage logs

---

## ⚠️ Notes

* Never allow all ports in a real production environment
* Always use IAM roles, SSH key security, and private IPs for internal traffic
* Jenkins and Tomcat credentials must be stored securely

---

## 💼 Author

**Confideo IT Services**

For training, corporate setup, and DevOps consulting — visit our profile or contact via GitHub.

---

```

Would you like this as a downloadable `README.md` file?
```
