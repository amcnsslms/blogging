pipeline {
    agent any

    stages {
        stage('Cloning GIT') {
            steps {
                sh 'rm -Rf blogging'
                sh 'git clone https://github.com/amcnsslms/blogging.git'
                sh 'ls -ltr blogging'
            }
        }
        
        stage('Building docker image') {
           steps {
               sh 'cd blogging && sudo docker build -t susigughimg .'
               sh 'sudo docker images'
           } 
        }
        stage('Run Container') {
            steps {
                sh 'sudo docker stop blog01 && sudo docker rm blog01'
                sh 'sudo docker run -dit --name="blog01" -p8081:8080 susigughimg'
            }
        }
    }

    post {
    success {
    sh 'echo "Successful"'
    }
    }
}
