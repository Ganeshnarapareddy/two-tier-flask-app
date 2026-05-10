# Two-Tier Flask Application with Jenkins CI/CD Pipeline

A robust, containerized two-tier web application featuring a Flask frontend and a MySQL database. This project demonstrates a complete DevOps lifecycle, from local development to automated deployment on AWS using Jenkins and Docker Compose.

🚀 Architecture Overview
This project follows a classic two-tier architecture:

Application Tier: A Python Flask application serving the web interface and handling API requests.

Database Tier: A MySQL 5.7 instance for persistent data storage.

Infrastructure: Hosted on an AWS EC2 (Amazon Linux 2023) instance.

CI/CD: Automated via a Jenkins Pipeline that pulls code from GitHub and orchestrates the deployment using Docker Compose.

🛠 Tech Stack
Language: Python 3.9 (Flask)

Database: MySQL 5.7

Automation: Jenkins (Pipeline-as-Code)

Containerization: Docker & Docker Compose

Cloud: AWS EC2 (Amazon Linux 2023)

📋 Prerequisites
To replicate this environment, ensure the following are installed on your EC2 instance:

Java 21: Required for Jenkins.

Docker & Docker Compose Plugin: For container orchestration.

Git: To allow Jenkins to clone the repository.

🔧 Installation & Setup
1. Server Preparation
On your Amazon Linux EC2 instance, install the core components:

# Install Java 21 and Jenkins
sudo dnf install java-21-amazon-corretto jenkins -y

# Install Docker & Compose
sudo dnf install docker docker-compose-plugin -y
sudo systemctl enable --now docker

# Add Jenkins to the Docker group
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
2. Memory Optimization (Crucial for t2.micro)
To prevent the server from freezing during Docker builds, it is recommended to set up a 2GB Swap file:

sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

🏗 CI/CD Pipeline Configuration
Unlock Jenkins: Retrieve the initial password using sudo cat /var/lib/jenkins/secrets/initialAdminPassword.

Adjust Node Thresholds: In Manage Jenkins > Nodes > Built-In Node > Configure, set Free Temp Space to 100MiB and Free Disk Space to 500MiB.

Create Pipeline:

Create a new Pipeline project named Two-Tier-App.

Under Pipeline, select Pipeline script from SCM.

Repository URL: Your GitHub repo URL.

Branch: */master.

Run Build: Click Build Now.

🌐 Accessing the App
Once the pipeline finishes with a SUCCESS status:

Open Port 5000 in your AWS EC2 Security Group.

Navigate to http://<EC2-Public-IP>:5000 in your browser.

📝 Troubleshooting
Docker Permissions: If Jenkins fails during the "Deploy" stage, ensure the Jenkins user is in the Docker group (sudo usermod -aG docker jenkins).

Java Version: Jenkins requires LTS versions (17 or 21). Use alternatives --config java to switch if necessary.

Node Offline: If the node goes offline due to disk space, lower the monitoring thresholds in Jenkins settings.
