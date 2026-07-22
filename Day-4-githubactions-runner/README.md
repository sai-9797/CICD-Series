So Iâll give you a proper README.md explaining this clearly (with comparison) ð

# ð GitHub Actions Architecture (Runner-Based)

---

## ð What is GitHub Actions?

GitHub Actions is a CI/CD automation tool provided by GitHub to build, test, and deploy applications directly from your repository.

---

## â ï¸ Master-Slave vs GitHub Actions

In tools like Jenkins:
- **Master** â Controls pipelines  
- **Slave (Agent)** â Executes jobs  

ð GitHub Actions uses a different architecture:

---

## ð§  GitHub Actions Architecture

### ð¹ 1. Workflow
- Defined in `.github/workflows/*.yml`
- Contains jobs and steps

---

### ð¹ 2. Runner

A **Runner** is a machine that executes jobs.

Types of runners:

#### â GitHub-Hosted Runner
- Managed by GitHub  
- Example:
```yaml
runs-on: ubuntu-latest
â Self-Hosted Runner
Your own server (EC2, VM, local machine)
You install runner manually
ð Execution Flow
Developer Push / Manual Trigger
            â
     GitHub Actions Workflow
            â
         Job Created
            â
      Runner Picks Job
            â
     Executes Steps
            â
        Output Logs
âï¸ Example Workflow
name: Sample Pipeline

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Print Message
        run: echo "Hello from GitHub Actions"
ð¥ï¸ Self-Hosted Runner Setup
Step 1: Go to Repository
Settings â Actions â Runners
Step 2: Add New Runner
Choose OS (Linux / Windows / Mac)
Step 3: Run Commands on Your Server
# Download runner
mkdir actions-runner && cd actions-runner

# Download package (example)
curl -o actions-runner.tar.gz -L https://github.com/actions/runner/releases/latest/download/actions-runner-linux-x64.tar.gz

# Extract
tar xzf ./actions-runner.tar.gz

# Configure
./config.sh --url https://github.com/your-repo --token YOUR_TOKEN

# Start runner
./run.sh
ð Using Self-Hosted Runner in Workflow
jobs:
  build:
    runs-on: self-hosted

ð You can also use labels:

runs-on: [self-hosted, linux, dev]
