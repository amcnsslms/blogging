pipeline {
    agent any
    stages {

        stage('Send Dockerfile to docker server') {
            steps {
		sh 'scp -o StrictHostKeyChecking=no Dockerfile ec2-user@43.204.32.168:/home/ec2-user/'
            }
        }
    }
}


