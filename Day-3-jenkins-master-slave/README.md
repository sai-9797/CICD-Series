# ð Jenkins Master-Slave (Controller-Agent) Architecture

---

## ð What is Jenkins?

Jenkins is an open-source automation server used to implement CI/CD pipelines.

It helps to:
- Build applications  
- Run tests  
- Deploy code automatically  

---

## ð§  Jenkins Architecture

Jenkins follows a **Master-Slave architecture** (now called **Controller-Agent**).

---

## ð¹ Components

### 1ï¸â£ Master (Controller)

The **Master** is the main Jenkins server.

Responsibilities:
- Manage pipelines (jobs)
- Schedule builds
- Monitor execution
- Assign jobs to agents
- Provide UI (dashboard)

---

### 2ï¸â£ Slave (Agent)

The **Slave (Agent)** is a worker machine.

Responsibilities:
- Execute build jobs
- Run scripts and commands
- Handle workload from master

ð Agents can be:
- Linux machines  
- Windows machines  
- Cloud instances (AWS EC2, etc.)

---

## ð How It Works

```text
Developer Push Code
        â
   Jenkins Master
        â
 Assign Job to Agent
        â
   Agent Executes Job
        â
   Send Result to Master
        â
   Display in Dashboard
