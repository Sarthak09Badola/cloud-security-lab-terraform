# DevSecOps & Advanced Data Protection: Encrypted S3 with CI/CD Validation

## 🎯 Project Objective
This project evolves a foundational AWS S3 deployment into an enterprise-grade **DevSecOps** pipeline. It demonstrates how to implement "Shift-Left" security principles, ensuring infrastructure is secure by design and continuously validated through automated CI/CD workflows.

## 🛠️ Tech Stack
* **Cloud Simulation:** LocalStack v1.4.0 (via Docker)
* **Infrastructure as Code (IaC):** Terraform (AWS Provider v5)
* **Security Linting:** tfsec (Automated IaC scanning)
* **CI/CD Pipeline:** GitHub Actions
* **CLI:** AWS CLI v2

## 🚀 Key Security Features Implemented

### 1. Advanced Data Protection
* **Server-Side Encryption (SSE-S3 / AES-256):** Enforces default encryption for all objects, ensuring data-at-rest is unreadable to unauthorized users.
* **Bucket Versioning:** Implements object versioning to provide a robust recovery mechanism against accidental deletions or ransomware attacks.

### 2. Automated Security Guardrails (Shift-Left)
* Integrated **tfsec** to automatically scan Terraform code for security misconfigurations (e.g., public buckets, missing encryption) *before* deployment.
* Implemented **Accepted Risk** tags (`# tfsec:ignore`) to document deliberate architectural decisions (e.g., using AWS-managed keys for this specific lab environment vs. KMS).

### 3. Hands-Off CI/CD Pipeline
* Built a **GitHub Actions** workflow (`.github/workflows/terraform.yml`) that automatically runs on every Push and Pull Request.
* The pipeline enforces code quality (`terraform fmt`), validates syntax (`terraform validate`), and executes the `tfsec` security audit without human intervention.

## 🏗️ How to Run Locally
1. Ensure Docker is running and the LocalStack container is active.
2. Set LocalStack environment variables: `export AWS_ACCESS_KEY_ID=test AWS_SECRET_ACCESS_KEY=test AWS_DEFAULT_REGION=us-east-1`
3. Deploy the infrastructure: `terraform apply -auto-approve`
4. Verify security controls using the AWS CLI with the LocalStack endpoint.
