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
               // sh 'sudo docker stop blog01 && sudo docker rm blog01'
                sh 'sudo docker run -dit --name="blog01" -p8081:8080 susigughimg'
		sh 'sudo docker stop blog01 && sudo docker rm blog01'
            }
        }

	stage('Tag the image') {
	steps {
	sh 'sudo docker image tag susigughimg 6esusigugh/susigughimg:0109'
	}
	}

	stage('Push image to dockerbub') {
	steps {
        withCredentials([usernamePassword(
            credentialsId: 'dockerhub-creds',
            usernameVariable: 'DOCKER_USERNAME',
            passwordVariable: 'DOCKER_PASSWORD'
        )]) {
            sh 'echo "$DOCKER_PASSWORD" | sudo docker login -u "$DOCKER_USERNAME" --password-stdin && sudo docker push "$DOCKER_USERNAME/susigughimg:0109"'
        }
    }
    }


    stage('push kubernetes files') {
    steps {
    sh 'scp blogging/blog.yaml ec2-user@172.31.36.41:/home/ec2-user/'
}
}


stage('Deploy blog.yaml') {
steps {

sh 'ssh ec2-user@172.31.36.41 && sudo kubectl delete -f /home/ec2-user/blog.yaml && sudo kubectl create -f /home/ec2-user/blog.yaml'

}
}

    }

    post {
    success {
    sh 'echo "Successful"'
    }
    }
}
