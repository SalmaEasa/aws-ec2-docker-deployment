# eMart E-Commerce Platform - Dockerized 🛒

This repository contains a full-stack e-commerce application, **eMart**, containerized using Docker and deployed on **AWS EC2**.

### Architecture Diagram
![Architecture Diagram](./Diagrams/EMart App Architecture.png)

## 🏗️ Architecture
The application follows a microservices architecture orchestrated with **Docker Compose**:
* **Frontend:** Angular application served via **Nginx**.
* **Java API:** Spring Boot backend for business logic.
* **Node API:** Node.js backend service.
* **CI/CD:** Jenkins pipeline for automated deployments.

---

## 🛠️ Infrastructure & Memory Optimization
To successfully deploy on low-resource environments like **AWS Free Tier (t3.micro)**, the following optimizations were implemented:

* **Memory Extension:** Configured **2GB Swap Space** to handle resource-heavy Angular builds.
* **Build Tuning:** Applied `--max-old-space-size=1024` to the Node engine during the Angular build process to prevent OOM (Out of Memory) crashes.
* **Multi-stage Docker Builds:** Implemented to ensure slim production images and efficient layer caching.

---

## 🚀 Getting Started

### Prerequisites
* AWS EC2 instance (t3.micro or higher).
* Docker and Docker Compose installed.
* Security Group configured to allow traffic on port 80.

### Installation & Deployment
```bash
# Clone the repository
git clone [https://github.com/YourUsername/emart-ecommerce-dockerized.git](https://github.com/YourUsername/emart-ecommerce-dockerized.git)
cd emart-ecommerce-dockerized

# Build and run the application
docker compose build
docker compose up -d
📂 Project Structure
The project is organized into microservices, each with its own environment and dependencies:

Plaintext
EMARTAPP/
├── client/             # Angular Frontend (Port 4200)
├── nodeapi/            # Node.js Authentication Service (Port 5000)
├── javaapi/            # Java/Spring Boot Product Service (Port 9000)
├── nginx/              # Reverse Proxy configuration (Port 80)
├── DIAGRAMS/           # Project architecture and visual diagrams 🖼️
│   └── EMart App Architecture.png
├── kkartchart/         # Deployment Helm charts / additional configs
├── docker-compose.yaml # Main orchestration file
├── Jenkinsfile         # CI/CD Pipeline automation
└── README.md           # Project documentation
Developed by [Salma Easa]