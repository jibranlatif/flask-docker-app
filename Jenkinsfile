pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-docker-app"
        CONTAINER_NAME = "flask-app"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/jibranlatif/flask-docker-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop and Remove Existing Container') {
            steps {
                sh '''
                if [ $(docker ps -q -f name=$CONTAINER_NAME) ]; then
                    docker stop $CONTAINER_NAME
                fi
                if [ $(docker ps -aq -f name=$CONTAINER_NAME) ]; then
                    docker rm $CONTAINER_NAME
                fi
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }
    }
}

