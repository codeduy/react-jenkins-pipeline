# 🚀 Automated CI/CD Pipeline for React Dashboard (Vision UI)

## 📌 Project Overview
This repository serves as a practical demonstration of an **end-to-end CI/CD (Continuous Integration & Continuous Deployment) pipeline** designed for a modern Frontend application (ReactJS).
The primary focus of this project is not on the UI development itself, but on **automating the Build and Deploy processes** utilizing **Jenkins** and Linux system administration practices. 

## 🛠 Technologies & Tools
- **Frontend Framework:** ReactJS (MUI, Vision UI Template)
- **CI/CD Automation:** Jenkins (Declarative Pipeline)
- **Web Server / Runtime:** Node.js, `serve` package
- **OS & Environment:** Linux, Bash Scripting
- **Process Management:** `fuser`, `nohup`

## 🔄 Pipeline Architecture (Jenkinsfile)
The CI/CD workflow is orchestrated via a Declarative Jenkins Pipeline divided into three automated stages:

1. **Stage 1: System Info (Environment Audit)**
   - Audits and outputs the worker node details (`whoami`, `pwd`, file listing). Ensures the pipeline is executing on the correct Jenkins Agent.
2. **Stage 2: Build Application**
   - Automatically resolves underlying dependencies via `npm install`.
   - Compiles and optimizes the React source code (`npm run build`) for the Production environment.
3. **Stage 3: Zero-ish Downtime Deployment**
   - **Port Release:** Automatically frees TCP port 3000 (`fuser -k 3000/tcp`) to prevent collision errors during new deployments.
   - **Background Deployment:** Deploys the application as a detached background process using `nohup serve ... &`.
   - **Process Lifecycle Management:** Utilizes the `JENKINS_NODE_COOKIE=dontKillMe` environment variable trick to prevent Jenkins from aggressively terminating the deployed background process after the job finishes.

## 💡 Key Learnings & Skills Demonstrated
- Jenkins Agent configuration and Environment Variables management.
- Infrastructure problem-solving: Handling ghost processes, releasing hanging TCP ports.
- Bash scripting integration inside Jenkins Pipelines to execute raw OS-level commands automatically.

## 🚀 How to Run Locally via Jenkins
1. Set up Jenkins and configure an active Agent/Node.
2. Create a new **Pipeline Job** in Jenkins and link this Git repository.
3. Trigger the Build.
4. Access the newly deployed dashboard at `http://<your-server-ip>:3000`.

## 📸 CI/CD Pipeline Results
> **Note:** Below are the screenshots showcasing the successful execution of the declarative Jenkins Pipeline and the resulting application deployment.

**1. Jenkins Pipeline Execution:**
![Jenkins Pipeline Result](./public/images/jenkins-success.png)

**2. Application Active on Listening Port:**
![Netstat Result](./public/images/port-listening.png)

---
*Disclaimer: The base UI frontend template is provided by [Creative Tim](https://www.creative-tim.com/). This repository is a modified version purposed exclusively for demonstrating DevOps and CI/CD configurations.*
