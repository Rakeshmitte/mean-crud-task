# 🚀 MEAN CRUD Task

This repository contains a **MEAN stack (MongoDB, Express, Angular, Node.js)** CRUD application with **Docker-based deployment** and **CI/CD automation**.  
The project demonstrates how to containerize the frontend and backend, manage services with Docker Compose, and deploy to a cloud VM (AWS EC2).  

---

## 📌 Project Structure

mean-crud-task/
├── backend/ # Node.js + Express backend
│ └── Dockerfile
├── frontend/ # Angular frontend
│ └── Dockerfile
├── docker-compose.yml # Service definitions (frontend, backend, mongo, nginx)
├── nginx.conf # Reverse proxy config
├── Jenkinsfile # Jenkins CI/CD (optional)
├── .github/workflows/ # GitHub Actions CI/CD
└── README.md


yaml
---

## ⚙️ Tech Stack

- **Frontend** → Angular  
- **Backend** → Node.js + Express  
- **Database** → MongoDB  
- **Reverse Proxy** → Nginx  
- **Containerization** → Docker & Docker Compose  
- **CI/CD** → GitHub Actions / Jenkins  
- **Cloud Deployment** → AWS EC2 (Ubuntu)  

---

## 🐳 Docker Setup (Local)

### 1️⃣ Build and Run with Docker Compose
```bash
# Clone repository
git clone https://github.com/Rakeshmitte/mean-crud-task.git
cd mean-crud-task

# Build images
docker compose build

# Start containers
docker compose up -d

#verify running contaoners
docker ps

#port numbers
Frontend → port 80

Backend → port 8080

MongoDB → port 27017

Nginx → proxying requests
-----------------------------------------------------------------------------------------------------
Deployment on AWS EC2
1️⃣ Launch Ubuntu EC2 instance

Open ports: 80, 8080, 27017 in Security Groups.

SSH into the server.

2️⃣ Install Docker & Docker Compose
sudo apt update
sudo apt install -y docker.io docker-compose
sudo systemctl enable docker
sudo systemctl start docker
3️⃣ Deploy Application
git clone https://github.com/Rakeshmitte/mean-crud-task.git
cd mean-crud-task
sudo docker compose up -d

4️⃣ Verify
sudo docker ps
-------------------------------------------------------------------------------------------------
#Access in browser:

Frontend (Angular UI) → http://<EC2-Public-IP>/

Backend API → http://<EC2-Public-IP>:8080/api

-----------------------------------------------------------------------------------------------------

🌐 Nginx Setup

nginx.conf:

server {
    listen 80;

    location / {
        proxy_pass http://frontend:80;
    }

    location /api/ {
        proxy_pass http://backend:8080/;
    }
}


This ensures:

Frontend served on /

Backend APIs proxied through /api
--------------------------------------------------------------------------------------------------------
🔄 CI/CD Pipeline

We use GitHub Actions to build & push Docker images to Docker Hub.

.github/workflows/ci-cd.yml:

Trigger: push to main

Steps: checkout → build Docker images → push to Docker Hub

Jenkins alternative:

Jenkinsfile is included for Jenkins-based pipelines.



[![Image](https://github.com/user-attachments/assets/63a8232f-ed30-447b-b8f6-c33b823fcdbb)](https://github.com/user-attachments/assets/63a8232f-ed30-447b-b8f6-c33b823fcdbb)



