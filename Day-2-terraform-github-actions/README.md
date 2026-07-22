# ð GitHub Actions + Terraform CI/CD Pipeline

---

## ð What is GitHub Actions?

GitHub Actions is a CI/CD tool that allows you to automate build, test, and deployment workflows directly from your GitHub repository.

---

## ð What is a Pipeline?

A pipeline is a sequence of automated steps:

1. Fetch code  
2. Build / Validate  
3. Test  
4. Deploy  

ð In GitHub Actions, pipelines are called **Workflows**

---

## ð How to Create GitHub Actions YAML File

1. Go to your repository  
2. Create a folder:


.github/workflows/


3. Inside that folder, create a file:


terraform.yml


---

## â¡ Workflow Triggers

### ð¹ 1. Manual Trigger

```yaml
on:
  workflow_dispatch:

ð Run manually from GitHub UI

ð¹ 2. Push Trigger
on:
  push:
    branches:
      - main

ð Runs automatically when code is pushed to main branch

ð¹ 3. Both Manual + Push
on:
  push:
    branches:
      - main
  workflow_dispatch:

ð Supports both automatic and manual execution

ð Terraform Pipeline (Basic)
name: Terraform Deploy

on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  terraform:
    runs-on: ubuntu-latest

    env:
      AWS_ACCESS_KEY_ID: \${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: \${{ secrets.AWS_SECRET_ACCESS_KEY }}
      AWS_DEFAULT_REGION: us-east-1

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v3

      - name: Terraform Init
        run: terraform init

      - name: Terraform Validate
        run: terraform validate

      - name: Terraform Plan
        run: terraform plan -out=tfplan

      - name: Terraform Apply
        run: terraform apply -auto-approve tfplan
ð§¾ Steps Explanation
Checkout Code â Downloads repository code
Setup Terraform â Installs Terraform CLI
Init â Initializes Terraform
Validate â Checks syntax errors
Plan â Shows changes
Apply â Deploys infrastructure
ð Manual Approval (Production Safe)

GitHub Actions doesnât use input like Jenkins. Instead, use environments.

Step 1: Add Environment in Workflow
jobs:
  terraform:
    runs-on: ubuntu-latest
    environment: production
Step 2: Configure in GitHub
Go to Settings â Environments
Create environment: production
Add Required reviewers

ð Pipeline will pause until approval is given

ð Advanced Pipeline with Approval
name: Terraform Deploy with Approval

on:
  workflow_dispatch:

jobs:
  terraform:
    runs-on: ubuntu-latest
    environment: production

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v3

      - name: Init
        run: terraform init

      - name: Plan
        run: terraform plan

      - name: Apply
        run: terraform apply -auto-approve

ð Approval required before Apply stage runs

ð Best Practices
Use GitHub Secrets for credentials
Avoid -auto-approve in production
Use remote backend (S3 + DynamoDB)
Separate environments (dev / stage / prod)
Enable approval for production
ð Workflow Execution Flow
Push / Manual Trigger
        â
Checkout Code
        â
Setup Terraform
        â
Init
        â
Validate
        â
Plan
        â
Approval (if enabled)
        â
Apply
