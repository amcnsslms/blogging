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
        stage('Run Container and remove') {
            steps {
                sh 'sudo docker stop blog01 && sudo docker rm blog01'
                sh 'sudo docker run -dit --name="blog01" -p8081:8080 susigughimg'
		sh 'sudo docker stop  blog01 && sudo docker rm blog01'
            }
        }

	stage('Tag the image') {
	steps {
	sh 'sudo docker image tag susigughimg 6esusigugh/susigughimg:0109'
	}
	}

/*	stage('Push image to dockerbub') {
	steps {
        withCredentials([usernamePassword(
            credentialsId: 'dockerhub-creds',
            usernameVariable: 'DOCKER_USERNAME',
            passwordVariable: 'DOCKER_PASSWORD'
        )]) {
            sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin && docker push "$DOCKER_USERNAME/susigughimg:0109"'
        }
    }
    }*/


    }

    post {
    success {
    sh 'echo "Successful"'
    }
    }
}
