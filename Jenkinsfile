pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub' // The ID of the DockerHub credentials
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/NUCESFAST/scd-final-lab-exam-Rayyan-Attaullah'
            }
        }

        stage('Install Dependencies') {
    steps {
        dir('Auth') {
            bat 'npm.cmd install'
        }
        dir('Classroom') {
            bat 'npm.cmd install'
        }
        dir('Post') {
            bat 'npm.cmd install'
        }
        dir('EventBus') {
            bat 'npm.cmd install'
        }
        dir('client') {
            bat 'npm.cmd install'
        }
    }
}


        stage('Build and Push Docker Images') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: env.DOCKER_CREDENTIALS_ID, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        docker.build('rayyanatttaullah09/auth:latest', './Auth')
                        docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                            docker.image('rayyanatttaullah09/auth:latest').push('latest')
                        }

                        docker.build('rayyanatttaullah09/classroom:latest', './Classroom')
                        docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                            docker.image('rayyanatttaullah09/classroom:latest').push('latest')
                        }

                        docker.build('rayyanatttaullah09/post:latest', './Post')
                        docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                            docker.image('rayyanatttaullah09/post:latest').push('latest')
                        }

                        docker.build('rayyanatttaullah09/event-bus:latest', './EventBus')
                        docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                            docker.image('rayyanatttaullah09/event-bus:latest').push('latest')
                        }

                        docker.build('rayyanatttaullah09/client:latest', './client')
                        docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                            docker.image('rayyanatttaullah09/client:latest').push('latest')
                        }
                    }
                }
            }
        }

        stage('Deploy Containers') {
            steps {
                sh 'docker-compose -f docker-compose.yml up -d'
            }
        }
    }
}
