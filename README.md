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
![Jenkins Pipeline Result](./public/images/jenkins-success.png)

**2. Application Active on Listening Port:**
![Netstat Result](./public/images/port-listening.png)

## 🚀 How to Run It Yourself
1. Set up Jenkins on your server.
2. Create a new Jenkins Pipeline job and connect it to this GitHub repository.
3. Click "Build Now" and wait for it to complete.
4. Enjoy your deployed app at `http://<your-server-ip>:3000` (or check your server's open ports).

---
*Note: The original frontend UI template is from [Creative Tim](https://www.creative-tim.com/). This repository is mainly built to practice Jenkins and CI/CD.*
