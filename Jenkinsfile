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
        HARBOR_REGISTRY = '192.168.1.35'
        HARBOR_PROJECT = 'sosyal_plaka'
        DOCKER_CREDENTIALS = 'harbor-credentials-id' // Jenkins'de tanımlanan kimlik bilgisi ID'si
        USERNAME = 'robot$sosyal_plaka'
        PASSWORD = 'fspMntyMnXq1qDWlx6bioTRV6AIhQgNg'
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
        stage("Build Docker Image") {
            steps {
                script {
                    dockerImage = docker.build("${HARBOR_REGISTRY}/${HARBOR_PROJECT}/${APP_NAME}:${BUILD_NUMBER}")
                }
            }
        }
        stage("Push Image") {
            steps {
                script {
                    docker login "${HARBOR_REGISTRY}/${HARBOR_PROJECT}" -u ${USERNAME} -p ${PASSWORD}
                docker push "${HARBOR_REGISTRY}/${HARBOR_PROJECT}":${BRANCH}-${GIT_COMMIT_SHORT}-${BUILD_DATETIME}-${BUILD_NUMBER}

                    }
                }
            }
        }
    }
}
