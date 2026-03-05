# CI/CD Pipeline using GitHub Actions for Java Application

## Project Overview

This project demonstrates a **complete CI/CD pipeline implemented using GitHub Actions for a Java Maven application**. The pipeline automates the process of **compiling the code, performing security scans, running unit tests, analyzing code quality with SonarCloud, and building & pushing a Docker image to DockerHub**.

The workflow is triggered automatically whenever code is pushed to the **main branch**, ensuring continuous integration and automated delivery.

This project follows **DevSecOps practices** by integrating security scanning tools such as **Trivy and Gitleaks** within the pipeline.

---

## CI/CD Pipeline Stages

The GitHub Actions workflow consists of the following stages:

### 1. Compile Stage

* Checks out the repository code
* Sets up **Java 17 environment**
* Compiles the Maven project using:

```
mvn clean compile
```

Purpose: Ensure the application compiles successfully before further stages.

---

### 2. Security Scan Stage

This stage performs security checks on the repository.

Tools used:

**Trivy**

* Scans the project filesystem for vulnerabilities.

**Gitleaks**

* Detects accidentally committed secrets such as API keys, tokens, or passwords.

These scans help enforce **secure coding practices** early in the CI pipeline.

---

### 3. Unit Test Stage

Runs automated tests written for the application.

Command used:

```
mvn test
```

Purpose:

* Validate application functionality
* Prevent broken code from progressing further in the pipeline.

---

### 4. Build + SonarCloud Code Analysis

In this stage:

1. The application is packaged into a **JAR file** using Maven:

```
mvn clean package
```

2. Code quality analysis is performed using **SonarCloud**, which checks for:

* Bugs
* Code smells
* Security vulnerabilities
* Maintainability issues

SonarCloud helps maintain **high code quality standards**.

---

### 5. Docker Build and Push Stage

In the final stage, the application is containerized.

Steps performed:

1. Build the JAR file again

```
mvn clean package -DskipTests
```

2. Verify the JAR file exists inside the `target` folder.

3. Authenticate with **DockerHub** using repository secrets.

4. Build a Docker image:

```
docker build -t h2004/bankapp:latest .
```

5. Push the Docker image to DockerHub:

```
docker push h2004/bankapp:latest
```

This enables the application to be deployed easily using containers.

---

## Workflow File Location

```
.github/workflows/cicd.yml
```

The workflow is triggered when code is pushed to:

```
main branch
```

---

## Technologies Used

* GitHub Actions
* Java 17
* Maven
* Docker
* DockerHub
* SonarCloud
* Trivy
* Gitleaks

---

## Required GitHub Secrets and Variables

### Secrets

Configure the following in **GitHub Repository → Settings → Secrets**:

* `SONAR_TOKEN`
* `DOCKERHUB_TOKEN`

### Variables

Configure repository variables:

* `DOCKERHUB_USERNAME`

---

## Project Structure

```
project-folder
│
├── src/
├── target/
├── Dockerfile
├── pom.xml
├── .github
│   └── workflows
│       └── cicd.yml
└── README.md
```

---

## Pipeline Workflow

Code Push → Compile → Security Scan → Unit Test → SonarCloud Analysis → Docker Build → Docker Push

This automated pipeline ensures that every code change is **tested, scanned for vulnerabilities, analyzed for quality, and packaged into a deployable Docker image**.

---

## Key Features

* Automated CI/CD pipeline
* DevSecOps integration
* Code quality analysis with SonarCloud
* Containerized application deployment
* Secure DockerHub authentication using GitHub Secrets

---

## Author

Hari
