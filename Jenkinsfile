pipeline {
    agent {
        label 'Jenkins-Agent'
    }
    
    environment {
        appUser = "jenkins"
        appName = "vision"
        appVersion = "1.0.0" 
        appType = "react" 
    }
    
    stages {
        stage('info') {
            steps {
                sh(script: """ 
                    echo "Checking system information..."
                    whoami; pwd; ls -la 
                """, label: "System Information")
            }
        }
        
        stage('build') {
            steps {
                echo "Building [${appName}] version [${appVersion}] (Type: ${appType})..."
                sh(script: """ 
                    echo "=> Installing dependencies..."
                    npm install
                    
                    echo "=> Running build..."
                    npm run build
                """, label: "Build React App")
            }
        }

        stage('deploy') {
            steps {
                echo "Deploying [${appName}]..."
                sh(script: """ 
                    echo "=> Killing old process on port 3000 (if any)..."
                    fuser -k 3000/tcp || true
                
                    JENKINS_NODE_COOKIE=dontKillMe nohup npx serve -s build -l 3000 > app.log 2>&1 &

                    echo "Deploy completed! App log is writing to app.log"
                """, label: "Deploy App")
            }
        }
    }
}
