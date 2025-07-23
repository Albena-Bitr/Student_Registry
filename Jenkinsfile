pipeline{
    agent any
    environment{
        NODE_VERSION = "24.4.1"
    }
    tools{
        nodejs "${NODE_VERSION}"
    }
    stages{
        stage('Checkout'){
            steps{
                checkout scm
            }
        }
        stage('Install dependencies'){
            steps{
                bat 'npm install'
                bat 'npm install -g wait-on kill-port'
            }
        }
        stage('Rum tests'){
            steps{
                bat 'start /b npm run start'
                bat 'wait-on http://localhost:8080'
                bat 'npm test'
                bat 'kill-port 8080'
            }
        }
    }
    post{
        always{
            echo 'CI Pipeline compleated'
        }
        failure{
            bat 'kill-port 8080'
        }
    }
}