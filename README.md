# 🚀 React Dashboard CI/CD Pipeline

## 📌 Introduction
This project is a simple demonstration of an automated **CI/CD pipeline** for a React application using **Jenkins**. 

While the frontend uses the Vision UI dashboard template, the main goal of this repository is to showcase how to automate the build and deployment process instead of doing it manually.

## 🛠 Tech Stack
- **Frontend:** ReactJS, Node.js (`serve`)
- **Automation:** Jenkins Pipeline
- **Environment:** Linux Server

## 🔄 How the Pipeline Works
The `Jenkinsfile` automatically runs the following steps:

1. **Check Environment (Info):** Prints basic info about the server (like `whoami`, `pwd`) to make sure the job is running on the correct machine.
2. **Build the App:** Runs `npm install` to get the dependencies and `npm run build` to create the production build.
3. **Deploy:** 
   - Finds and stops any old process running on port 3000 (`fuser -k 3000/tcp`).
   - Starts the app in the background using `nohup npx serve -s build -l 3000 > app.log 2>&1 &`.
   - Uses `JENKINS_NODE_COOKIE=dontKillMe` to prevent Jenkins from terminating the background app when the pipeline finishes.

## 📸 Screenshots

**1. Jenkins Pipeline Execution:**
<img width="1836" height="897" alt="image" src="https://github.com/user-attachments/assets/ede19d5d-69c6-4431-a89e-02932f85397e" />
<img width="1836" height="897" alt="image" src="https://github.com/user-attachments/assets/35d23020-3798-47e1-bd23-0b6fc31e853e" />



**2. Application Active on Listening Port:**
<img width="1046" height="594" alt="Screenshot from 2026-04-05 22-08-25" src="https://github.com/user-attachments/assets/eb2fcae7-6420-4a33-8d4d-db94ae9059bd" />

---
*Note: The original frontend UI template is from [Creative Tim](https://www.creative-tim.com/). This repository is mainly built to practice Jenkins and CI/CD.*
