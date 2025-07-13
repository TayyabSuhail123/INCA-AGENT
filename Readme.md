
## 🧭 What This Demo Includes

This project is split into two focused repositories:

### 1. Backend API

**Repo:** [`python-aws-api`](https://github.com/TayyabSuhail123/python-aws-api)  
**Contains:**  
- FastAPI backend service  
- Tests  
- Dockerfile  
- GitHub Actions pipeline (build → test → scan → push to ECR)

### 2. Infrastructure as Code

**Repo:** [`agent-runner-infra`](https://github.com/TayyabSuhail123/agent-runner-infra)  
**Contains:**  
- Terraform modules for VPC, subnets, ECS Fargate, ECR, IAM roles, and ALB  
- Secure state backend (S3 with state locking, using native S3 locking support in recent Terraform versions)

---

## 🚀 How to Review – No Local Setup Required

You don’t need to clone, fork, or configure anything.

✅ You already have **write access** to both repos  
✅ AWS credentials are securely injected via GitHub Secrets  
✅ The IAM user used is **limited to resource required** for demo purposes

---

## ⚠️ Important: Run Infra First

> **🚨 You must run the Terraform infra pipeline before triggering the Python API pipeline.**

The `python-aws-api` CI/CD workflow pushes its Docker image to an **ECR repository** that is created by the infrastructure repo.

If the ECR repo does not exist, the API pipeline will fail.

---

### 🔧 To Run the Full Pipeline:

1. Open the [`agent-runner-infra`](https://github.com/TayyabSuhail123/python-aws-api) repo  
   - Go to the **Actions** tab → select the **Terraform CI/CD workflow**  
   - Run the workflow to create the ECR repo and the rest of the infrastructure

2. While the infra is being provisioned (ECR repo is created almost instantly), open the [`python-aws-api`](https://github.com/TayyabSuhail123/python-aws-api) repo  
   - Go to the **Actions** tab → select **"Build, Test, Scan, and Push to ECR"**  
   - Click **“Run workflow”** on the `main` branch  
   - This builds, scans, and pushes the Docker image to the ECR repo


## ⚠️ Important: Destroy Infra after Demo
After demo is done please destroy all the Infra using the automated workflow Teraform Destroy.
Open the [`agent-runner-infra`](https://github.com/TayyabSuhail123/python-aws-api) repo
Go to the **Actions** tab → select the **Terraform Destroy workflow** and run the workflow to manually trigger Terraform Destroy.




Once the full infrastructure is up, you’ll receive the public URL to access the API and Swagger UI.
