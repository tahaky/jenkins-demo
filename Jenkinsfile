pipeline {
    agent any
    tools {
        maven "M3"
    }
    environment {
        APP_NAME = "jenkins-demo"
        RELEASE = "1.0.0"
        DOCKER_USER = "tahakaya"
        DOCKER_PASS = 'docker-id'
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
    }
    stages {
        stage("Clean Workspace") {
            steps {
                cleanWs()
            }
        }
        stage("Checkout F SCM") {
            steps {
                git branch: 'main', credentialsId: 'jenkins-github', url: 'https://github.com/tahaky/jenkins-demo'
            }
        }
        stage("Build") {
            steps {
                sh 'mvn clean package'
            }
        }
        stage("Test") {
            steps {
                sh 'mvn test'
            }
        }
        stage("Build & Push Docker Image") {
            steps {
                script {
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.build "${IMAGE_NAME}"
                    }

                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('latest')
                    }
                }
            }
        }
    }
}
