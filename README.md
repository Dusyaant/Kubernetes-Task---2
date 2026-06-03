# Docker Configuration: Containerized Profile Web Application

---

## Project Overview

This project contains the complete configuration and architectural components required to containerize a lightweight static web application. The application delivers a production-ready developer profile dashboard using responsive frontend components. The entire container infrastructure runs within an isolated environment, ensuring minimal host footprint while enabling public network access.

---

## Objective

The primary goal of Task 2 is to use standard Docker workflows to build, manage, and host a web service on a cloud instance.

### Milestones

* Create modular deployment configurations including custom static views, image specifications, and service configurations.
* Isolate service instances from overlapping cloud runtimes.
* Expose internal container processes to the public internet through standard network ports.

---

## Prerequisites

* **Cloud Platform Infrastructure:** AWS EC2 Instance
* **Host Operating System:** Amazon Linux 2023
* **Installed Engine:** Docker Engine (v25+)

### AWS Security Group Rules

| Type | Protocol | Port | Source    |
| ---- | -------- | ---- | --------- |
| HTTP | TCP      | 80   | 0.0.0.0/0 |

---

## Repository Structure

```text
Kubernetes-Task---2/
├── index.html
├── Dockerfile
└── docker-compose.yml
```

---

## Step-by-Step Implementation

### Step 1: Establish Workspace Directory

```bash
mkdir ~/docker-task-2
cd ~/docker-task-2
```

### Step 2: Create Frontend Page (`index.html`)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Developer Profile</title>
</head>
<body>
    <div class="card">
        <h1>Developer Profile</h1>
        <p><strong>Specialization:</strong> Computer Science Engineering (Cybersecurity)</p>
        <p><strong>Environment:</strong> Docker Containerization</p>
        <div class="badge">Deployment Status: Live</div>
    </div>
</body>
</html>
```

### Step 3: Create Dockerfile

```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
```

### Step 4: Create Docker Compose Configuration

```yaml
version: '3.8'

services:
  web-app:
    build: .
    container_name: student_profile_app
    ports:
      - "80:80"
    restart: always
```

---

## Commands Used

### Verify Project Files

```bash
ls -la
```

### Check Port Usage

```bash
sudo lsof -i :80
```

### Remove Existing Container

```bash
docker rm -f student_profile_container
```

### Stop Conflicting Services

```bash
minikube stop
sudo systemctl stop httpd
sudo systemctl stop nginx
```

### Build Docker Image

```bash
docker build -t developer-profile-app .
```

### Run Container

```bash
docker run -d -p 80:80 --name student_profile_container --restart always developer-profile-app
```

---

## Verification and Testing

### Check Running Containers

```bash
docker ps
```

### Expected Output

```text
CONTAINER ID   IMAGE                  STATUS         PORTS                  NAMES
332799e8629e   my-profile-app         Up 10 minutes  0.0.0.0:80->80/tcp   student_profile_app
```

### Access Application

```text
http://35.153.170.119
```

---

## Results

The application was successfully deployed on AWS EC2 using Docker and Nginx. Accessing the public IP address displays the developer profile page, confirming that HTTP requests are correctly routed to the containerized web application.

---

## Conclusion

Task 2 successfully demonstrated containerization of a static web application using Docker. The application was packaged into a portable image, deployed on an EC2 instance, and exposed through port 80, validating a simple and scalable deployment workflow.
](https://github.com/Dusyaant/Kubernetes-Task---2)
