pipeline {
    agent any
    tools {
        maven "M3"
    }
    environment {
        APP_NAME = "jenkins-demo"
        RELEASE = "1.0.0"
        DOCKER_USER = "tahakaya"
        HARBOR_REGISTRY = "192.168.1.35"
        HARBOR_PROJECT = "sosyal_plaka"
        DOCKER_CREDENTIALS = "harbor-credentials-id" // Jenkins'de tanımlanan kimlik bilgisi ID'si
        IMAGE_NAME = "${HARBOR_REGISTRY}/${HARBOR_PROJECT}/${APP_NAME}"
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
        stage("Build Docker Image") {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }
        stage("Push Image") {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS, usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        // Docker Login
                        sh """
                        echo $PASSWORD | docker login ${HARBOR_REGISTRY} -u $USERNAME --password-stdin
                        """
                        // Docker Push
                        sh """
                        docker push ${IMAGE_NAME}:${IMAGE_TAG}
                        docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${IMAGE_NAME}:latest
                        docker push ${IMAGE_NAME}:latest
                        """
                    }
                }
            }
        }
    }
}
