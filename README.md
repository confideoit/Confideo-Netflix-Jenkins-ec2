🎬 Netflix Clone CI/CD Deployment with Jenkins & Apache Tomcat on AWS

This project demonstrates how to build a complete **CI/CD pipeline** using Jenkins and Apache Tomcat on AWS EC2 instances to automate the deployment of a Netflix clone Java web application. This setup leverages DevOps best practices for continuous integration and delivery.

🔧 Technologies Used
- Jenkins (CI/CD automation)
- Apache Tomcat 9 (Application Server)
- AWS EC2 (Infrastructure hosting)
- Git & GitHub (Version control)
- Java 17 (Amazon Corretto)

📌 Project Overview
- Jenkins installed on one EC2 instance.
- Two EC2 instances configured with Apache Tomcat.
- WAR file deployment managed via Jenkins pipeline.
- Source code fetched from GitHub.
- Fully automated build-test-deploy cycle.

🛠️ Setup Instructions
1️⃣ Jenkins Setup
2️⃣ Tomcat Setup on Two Instances
3️⃣ Jenkins Configuration
4️⃣ Credentials & Plugins
5️⃣Jenkins Pipeline Configuration

🛠 Replace in Script
-	Replace the GitHub URL with your own repo if needed:
•	git url: 'https://github.com/YOUR_USERNAME/YOUR_REPO.git'
-	Update `credentialsId` with your generated Jenkins credential ID
-	Change Tomcat `url` to your own EC2 public IP

📥 Clone / Fork Repositories
1️⃣ Jenkins Project Repo:
  https://github.com/confideoit/Confideo-Netflix-Jenkins-ec2.git 
2️⃣ Jenkins & Tomcat Setup Scripts:
  https://github.com/confideoit/Confideo-All_Setup 

⚠️ Notes
-	Never allow all ports in a real production environment
-	Always use IAM roles, SSH key security, and private IPs for internal traffic
-	Jenkins and Tomcat credentials must be stored securely

💼 Author
Confideo IT Services
Providing industry-aligned DevOps training and cloud deployment solutions.
