pipeline {
    agent any
    stages {
        stage('Clone GIT Repository') {
            steps {
                sh 'rm -Rf jenkin01'
                sh 'git clone https://github.com/SUSIGUGH/jenkin01.git'
                sh 'ls -ltr jenkin01'
            }
        }
        
        stage('Build Docker Image 01') {
            steps {
            sh 'cd jenkin01 && sudo docker build -t susigugh . && sudo docker image ls'
            }
        }
        
    }
}

