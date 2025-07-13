---

## 🧭 What This Demo Includes

This project is split into two focused repositories:

### 1. Backend API

**Repo:** [`python-aws-api`](https://github.com/your-org/python-aws-api)  
**Contains:**  
- FastAPI backend service  
- Tests  
- Dockerfile  
- GitHub Actions pipeline (build → test → scan → push to ECR)

### 2. Infrastructure as Code

**Repo:** [`agent-runner-infra`](https://github.com/your-org/agent-runner-infra)  
**Contains:**  
- Terraform modules for VPC, subnets, ECS Fargate, ECR, IAM roles, and ALB  
- Secure state backend separation (Using only s3 for state locking as versions of Terraform allow state locking using s3)

---

## 🚀 How to Review – No Local Setup Required

You don’t need to clone, fork, or configure anything.

✅ You already have **write access** to the both repos. 
✅ AWS credentials are securely injected from GitHub Secrets  
✅ The IAM user used is **limited to ECR-only access** for demo purposes

## ⚠️ Important: Run Infra First

**🚨 You must run the Terraform infra pipeline before triggering the Python API pipeline.**

The `python-aws-api` project’s CI/CD pipeline pushes its Docker image to an **ECR repository** that is created by the Terraform infrastructure repo.

**If the ECR repo doesn’t exist yet, the pipeline will fail.**

---

### 🔧 To run the full pipeline:

1. Open the [`agent-runner-infra`](https://github.com/your-org/agent-runner-infra) repo  
   - Go to the **Actions** tab → Select the Terraform CI/CD
   - This creates the ECR repo and other necessary infra

2. Since the ECR repo will be created almost instatbtly its safe to open the [`python-aws-api`](https://github.com/your-org/python-aws-api) repo  
   - Go to the **Actions** tab → select **"Build, Test, Scan, and Push to ECR"**  
   - Click **“Run workflow”** (branch: `main`)  
   - The docker image will be pushed to the ECR repo

Now just wait until all the infra is created and you will get the url to access our Api/Swagger page.

