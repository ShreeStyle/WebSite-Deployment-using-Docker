# 🚀 Automated Website Deployment using Jenkins & Docker

A simple static website built with **HTML, CSS, and JavaScript** that demonstrates a complete **CI/CD pipeline using Jenkins and Docker**.

The primary goal of this project is to automate the deployment process. Whenever code is pushed to the Git repository, Jenkins automatically builds a Docker image, replaces the running container, deploys the latest version of the website, and verifies that the deployment was successful.

---

## 📌 Project Objective

This project demonstrates how Continuous Integration and Continuous Deployment (CI/CD) can automate the software delivery process.

Instead of manually rebuilding Docker images and restarting containers after every code change, Jenkins performs the entire workflow automatically.

---

## 🛠 Technologies Used

- HTML5
- CSS3
- JavaScript
- Docker
- Jenkins
- Apache HTTP Server (httpd)

---

## 📁 Project Structure

```
project/
│
├── HTML/
│   ├── index.html
│   ├── css/
│   ├── js/
│   └── images/
│
├── Dockerfile
├── Jenkinsfile
└── README.md
```

---

## 🐳 Docker Configuration

The application uses the official Apache HTTP Server image.

**Dockerfile**

```dockerfile
FROM httpd:2.4

COPY HTML/ /usr/local/apache2/htdocs/
```

The Docker image simply copies the static website into Apache's default web directory.

---

# ⚙ Jenkins Pipeline

The project uses a Declarative Jenkins Pipeline.

Pipeline stages include:

### 1. Checkout Source Code

Jenkins pulls the latest code from GitHub.

```
checkout scm
```

---

### 2. Build Docker Image

Builds a fresh Docker image every time new code is pushed.

```
docker build -t website-image .
```

---

### 3. Remove Existing Container

Stops and removes the previously running container.

```
docker rm -f website-container
```

Using `|| true` prevents the pipeline from failing if no previous container exists.

---

### 4. Deploy New Container

Runs the newly built Docker image.

```
docker run -d \
--name website-container \
-p 8081:80 \
website-image
```

The website becomes available on:

```
http://localhost:8081
```

---

### 5. Verify Deployment

Jenkins waits a few seconds and performs a health check.

```
curl http://localhost:8081
```

If HTTP Status Code **200** is returned, the deployment is considered successful.

Otherwise the pipeline fails.

---

# 🔄 CI/CD Workflow

```
Developer
     │
     │ Push Code
     ▼
GitHub Repository
     │
     ▼
Jenkins Job Triggered
     │
     ▼
Checkout Latest Code
     │
     ▼
Build Docker Image
     │
     ▼
Remove Old Container
     │
     ▼
Deploy New Container
     │
     ▼
Health Check
     │
     ▼
Website Live
```

---

# 🚀 How to Run Locally

### Clone Repository

```bash
git clone <repository-url>

cd <repository-name>
```

---

### Build Docker Image

```bash
docker build -t website-image .
```

---

### Run Container

```bash
docker run -d \
--name website-container \
-p 8081:80 \
website-image
```

---

### Open Website

```
http://localhost:8081
```

---

# 🔄 Automatic Deployment

Whenever changes are pushed to GitHub:

- Jenkins detects the latest code.
- Downloads the updated source.
- Builds a new Docker image.
- Removes the previous container.
- Deploys a new container.
- Tests the website automatically.
- Marks the build as Success or Failed.

No manual deployment is required.

---

# 📸 Jenkins Pipeline Flow

```
Git Push
   │
   ▼
Checkout
   │
   ▼
Docker Build
   │
   ▼
Remove Old Container
   │
   ▼
Run New Container
   │
   ▼
Health Check
   │
   ▼
Deployment Successful
```

---

# 🎯 Learning Outcomes

Through this project, I learned:

- Creating Docker images for static websites
- Writing Dockerfiles
- Working with Apache HTTP Server containers
- Creating Declarative Jenkins Pipelines
- Automating Docker deployments using Jenkins
- Managing Docker containers through Jenkins
- Implementing basic CI/CD workflows
- Performing automated deployment verification using health checks

---

# 👩‍💻 Author

**Dhanashree Trambadia**

DevOps Engineer | Docker | Jenkins | Linux | CI/CD | Git | GitHub