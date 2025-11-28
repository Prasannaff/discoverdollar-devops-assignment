# 🚀 Discover Dollar – DevOps Assignment

This repository contains the full DevOps implementation of a **MEAN Stack CRUD Application** deployed using:

- **Docker & Docker Compose**
- **Docker Hub**
- **NGINX Reverse Proxy**
- **AWS EC2 (Ubuntu 22.04)**
- **GitHub Actions (CI/CD Pipeline)**

The goal of the assignment is to **containerize**, **deploy**, and **automate** the application end-to-end.

---

# 📌 1. Application Overview

The application manages **Tutorials**, each containing:

- `id`
- `title`
- `description`
- `published` (boolean)

Users can:
- Create Tutorials  
- View Tutorials  
- Update Tutorials  
- Delete Tutorials  
- Search Tutorials by Title  

### 🧰 Technologies Used
| Layer | Technology |
|-------|------------|
| Frontend | Angular 15 |
| Backend | Node.js + Express.js |
| Database | MongoDB |
| Deployment | Docker, Nginx, AWS EC2 |
| CI/CD | GitHub Actions |

---

# 🛠️ 2. Local Development Setup

## 🔹 Backend (Node.js + Express)

```bash
cd backend
npm install
npm start
```
## Local backend URL:
👉 http://localhost:3000/

## To use local MongoDB:

bash
Copy code
MONGO_URI=mongodb://localhost:27017/tutorials
## 🔹 Frontend (Angular)
```bash
Copy code
cd frontend
npm install
ng serve --port 8081
```
## Open UI at:
👉 http://localhost:8081/

# 🐳 3. Dockerization
## 🔹 Build Backend Image
```bash
Copy code
docker build -t prasannff/dd-backend:latest -f backend/Dockerfile backend
```
## 🔹 Build Frontend Image
```bash
Copy code
docker build -t prasannff/dd-frontend:latest -f frontend/Dockerfile frontend
```
## 🔹 Push Images to Docker Hub
```bash
Copy code
docker login
docker push prasannff/dd-backend:latest
docker push prasannff/dd-frontend:latest
Docker Hub Links:
Backend → https://hub.docker.com/r/prasannff/dd-backend

Frontend → https://hub.docker.com/r/prasannff/dd-frontend
```
# 🧩 4. Docker Compose Deployment
```bash
Copy code
docker compose pull
docker compose up -d
```
Check containers:

```bash
Copy code
docker compose ps
```
This starts:

## MongoDB

## Backend API

## Frontend Angular build

## Nginx Reverse Proxy

# 🌐 5. AWS EC2 Deployment
## 1️⃣ Launch Ubuntu EC2
Ubuntu 22.04

t3.micro

2️⃣ SSH into Instance
```bash
Copy code
ssh -i your-key.pem ubuntu@<EC2_PUBLIC_IP>
```
## 3️⃣ Install Docker & Compose
(Installed during setup)

## 4️⃣ Clone Repo
bash
Copy code
git clone https://github.com/Prasannaff/discoverdollar-devops-assignment.git
cd discoverdollar-devops-assignment
## 5️⃣ Run Containers
```bash
Copy code
docker compose pull
docker compose up -d --remove-orphans
```
# App will be live at:
👉 http://<EC2_PUBLIC_IP>

## 🔁 6. NGINX Reverse Proxy
File: nginx/default.conf

nginx
Copy code
server {
    listen 80;

    location / {
        root /usr/share/nginx/html;
        try_files $uri $uri/ /index.html;
    }

    location /api {
        proxy_pass http://backend:3000;
    }
}
Serves Angular build

Routes /api → backend

## 🔄 7. GitHub Actions CI/CD
GitHub Actions pipeline performs:

✔ Build backend Docker image
✔ Build frontend Docker image
✔ Push images to Docker Hub
✔ SSH into EC2
✔ Pull updated images
✔ Restart containers automatically

Workflow file:

```bash
Copy code
.github/workflows/deploy.yml
```
Trigger:
✔ Runs automatically on every push to main

# 🔐 8. GitHub Secrets (Required)
Go to:
Repo → Settings → Secrets → Actions

Secret Name	Value
DOCKERHUB_USERNAME	prasannff
DOCKERHUB_TOKEN	Docker Hub Access Token
VM_HOST	<EC2_PUBLIC_IP>
VM_USER	ubuntu
VM_SSH_KEY	Full PEM private key content

# 📸 9. Required Screenshots
## 1️⃣ Docker Hub Images
Screenshot showing dd-backend and dd-frontend.
![Docker Hub Images](screenshots/dockerhub.png)

##  2️⃣ GitHub Actions – Successful CI/CD
![GitHub Actions Success](screenshots/github-actions.png)
##  3️⃣ EC2 – Running Containers
![EC2 Containers](screenshots/ec2-containers.png)
##  4️⃣ Live Application UI
![Nginx Config](screenshots/nginx-config.png)
##  5️⃣ NGINX Reverse Proxy Configuration

##  6️⃣ Repository Structure
![Repo Structure](screenshots/repo-structure.png)

✅ Completion
✔ Full MEAN application successfully containerized
✔ Automated CI/CD pipeline implemented
✔ Application deployed via NGINX on AWS EC2
✔ End-to-end DevOps workflow implemented

# 🙌 Thank You
This assignment demonstrates the complete DevOps lifecycle:
Build → Push → Deploy → Automate → Deliver.
Assignment Successfully Completed 🎉
