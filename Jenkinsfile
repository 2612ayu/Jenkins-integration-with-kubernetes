pipeline {

    triggers {
        githubPush()
    }
    environment {
        GIT_REPO = 'https://github.com/2612ayu/Jenkins-integration-with-kubernetes.git'
        BRANCH = 'main'
    }
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Docker Build') {
            steps {
                script { 
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        
        stage('Cleaning up') {
            steps {
                script {
                    sh "docker rmi -f $registry:$BUILD_NUMBER"
                }
            }
        }
    }
}

def fileExists(filePath) {
    def file = new File(filePath)
    return file.exists()
}
