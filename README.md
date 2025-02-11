![Starbucks Logo](https://github.com/prathamesh3146/Starbucks/blob/master/starbuck%20Logo.png)

# Deploy Starbucks Application Clone using DevSecOps Approach

## Overview
This project is a Starbucks web application clone that follows a **DevSecOps** approach using Jenkins for **Continuous Integration and Continuous Deployment (CI/CD)**. The deployment is **containerized with Docker** and orchestrated using **Docker Swarm**, ensuring high availability with **5 running replicas**.

## Features
- **Automated CI/CD pipeline** with Jenkins.
- **Static code analysis** using **SonarQube**.
- **Security vulnerability scanning** with **Trivy**.
- **Docker containerization** and deployment using **Docker Swarm**.
- **Ensures high availability** with **5 running replicas**.

## Prerequisites
### Jenkins Setup
1. Install Jenkins and required plugins:
   - **Pipeline Plugin**
   - **Git Plugin**
   - **SonarQube Scanner Plugin**
   - **Docker Pipeline Plugin**
2. Configure Jenkins tools in `Manage Jenkins` → `Global Tool Configuration`:
   - JDK 17 (`jdk17`)
   - Node.js 16 (`node16`)
   - Sonar Scanner (`sonar-scanner`)
3. Add **Jenkins credentials** in `Manage Credentials`:
   - `docker` → DockerHub credentials
   - `Sonar-token` → SonarQube authentication token
   - `mail-cred` → Email credentials

### Docker Setup
- Install **Docker** and **Docker Swarm** on the server.
- Run `docker swarm init` to initialize Swarm mode.
- Ensure Docker daemon is running with:
  ```sh
  systemctl enable --now docker
  ```

## Project Structure
```
Starbucks/
│── Jenkinsfile            # Jenkins pipeline script
│── Dockerfile             # Docker image build instructions
│── package.json           # Node.js dependencies
│── src/                   # Application source code
│── README.md              # Documentation (this file)
│── trivy.txt              # Trivy File scan report
│── Build.log              # Build logs 
│── Screenshots            # Screenshots of the project (optional)
```

## Jenkins Pipeline Workflow
1. **Pulls the latest code** from GitHub.
2. **Runs SonarQube analysis** to check code quality.
3. **Performs a security scan** using Trivy.
4. **Builds a Docker image** and pushes it to DockerHub.
5. **Deploys a Docker Swarm service** with **5 replicas**.
6. **Ensures containers restart automatically** if they fail.
7. **Sends an email** about the **success/failure of the Jenkins job pipeline** along with **build.log and Trivy scan report file.**

## Deployment
To manually deploy the application using Docker Swarm:
```sh
docker service create --name starbucks --replicas 5 \
  --publish 3000:3000 \
  --restart-condition any \
  prathamesh3146/starbucks:latest
```

## Accessing the Application
After deployment, access the application at:
```
http://<server-ip>:3000
```

### Verify Running Containers
```sh
docker service ls
docker container ls # Check whether the worker nodes are running
```

## Outputs
### SonarQube Code Analysis Report
![SonarQube Output](https://github.com/prathamesh3146/Starbucks/blob/master/Screenshot%20(293).png)

### Starbucks Website Output
![Starbucks Application](https://github.com/prathamesh3146/Starbucks/blob/master/Screenshot%20(294).png)

### Jenkins Pipeline Output
![Jenkins Pipeline 1](https://github.com/prathamesh3146/Starbucks/blob/master/Screenshot%20(295).png)
![Jenkins Pipeline 2](https://github.com/prathamesh3146/Starbucks/blob/master/Screenshot%20(296).png)

---
This **Starbucks Clone Deployment** project follows DevSecOps best practices to ensure **code quality, security, and scalability** while automating deployment with Jenkins and Docker Swarm.
