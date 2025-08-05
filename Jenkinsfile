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
		sh 'ssh -o StrictHostKeyChecking=no ec2-user@43.204.32.168 "cd /home/ec2-user && sudo docker build -t blog ."'
}
}


	stage('Run Blogging Site as Container from image') {
	     steps {
		sh 'ssh -o StrictHostKeyChecking=no ec2-user@43.204.32.168 "sudo docker run -dit -p3000:3000 blog"'
}
}


    }
}


