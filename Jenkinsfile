pipeline {
    agent any

    environment {
        DOCKER_HUB_USER = "rakesh402"    // your DockerHub username
        DOCKER_HUB_REPO_FRONTEND = "frontend"
        DOCKER_HUB_REPO_BACKEND = "backend"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Rakeshmitte/mean-crud-task.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_HUB_USER}/${DOCKER_HUB_REPO_FRONTEND}:latest ./frontend"
                    sh "docker build -t ${DOCKER_HUB_USER}/${DOCKER_HUB_REPO_BACKEND}:latest ./backend"
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh "echo $PASSWORD | docker login -u $USERNAME --password-stdin"
                }
            }
        }

        stage('Push Images') {
            steps {
                sh "docker push ${DOCKER_HUB_USER}/${DOCKER_HUB_REPO_FRONTEND}:latest"
                sh "docker push ${DOCKER_HUB_USER}/${DOCKER_HUB_REPO_BACKEND}:latest"
            }
        }

        stage('Deploy on EC2') {
            steps {
                sshagent(['ec2-ssh']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no ubuntu@44.211.127.124 "
                        cd ~/mean-crud-task &&
                        docker-compose pull &&
                        docker-compose up -d
                        "
                    '''
                }
            }
        }
    }
}

