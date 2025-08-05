pipeline {
    agent any
    stages {

        stage('Send Dockerfile to docker server') {
            steps {
		sh 'scp -o StrictHostKeyChecking=no Dockerfile ec2-user@43.204.32.168:/home/ec2-user/'
            }
        }
	
	stage('Create docker image in docker using the Docker') {
	     steps {
		sh 'ssh -o StrictHostKeyChecking=no ec2-user@43.204.168 "cd /home/ec2-user && sudo docker build -t blog ."'
}
}

    }
}


