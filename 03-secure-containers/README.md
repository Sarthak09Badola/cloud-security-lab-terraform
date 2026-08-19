# Project 3: Secure Containerization & Vulnerability Scanning Pipeline

## 🎯 Project Objective
While Project 1 and 2 secured the cloud infrastructure, Project 3 focuses on **Application Security**. If a developer builds an application using outdated software with known vulnerabilities (CVEs), hackers can bypass cloud firewalls and exploit the app directly. This project implements an automated "Shift-Left" security checkpoint to ensure no vulnerable code ever reaches the cloud.

## 🛠️ Tech Stack
* **Containerization:** Docker (Alpine Linux)
* **Security Scanning:** Trivy (Automated Container & CVE Scanning)
* **CI/CD Pipeline:** GitHub Actions
* **Cloud Simulation:** LocalStack v1.4.0

## 🚀 Key Security Features Implemented

### 1. Vulnerability Simulation & "On-The-Fly" Patching
* **The Threat:** Simulated a legacy application by deploying an intentionally outdated version of Nginx (1.19.0), which contained numerous Critical CVEs.
* **The DevSecOps Fix:** Upgraded to a lightweight `nginx:alpine` base image and injected `RUN apk update && apk upgrade` into the Dockerfile. This forces the container to patch its underlying operating system libraries *during the build process*, resulting in a 100% clean scan.

### 2. Automated CI/CD Security Gatekeeper
* Built a **GitHub Actions** workflow (`.github/workflows/docker-security.yml`) that acts as an automated bouncer.
* Integrated **Trivy** with the `--exit-code 1` flag.
* **The "Why":** Without this flag, a pipeline might print a warning but deploy the vulnerable container anyway. With `--exit-code 1`, if Trivy detects even a single Critical vulnerability, the pipeline instantly fails, blocking the code from being merged or deployed.

## 💡 Key Takeaways for Enterprise Security
* **Software Supply Chain Security:** Proves the ability to secure the actual software running inside the cloud, not just the perimeter.
* **Pipeline Parity & Automation:** Removes human error by enforcing security checks automatically on every single push and Pull Request.
