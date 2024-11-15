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
        HARBOR_REGISTRY = 'http://192.168.1.35/'
        HARBOR_PROJECT = 'sosyal_plaka'
        DOCKER_CREDENTIALS = 'harbor-credentials-id' // Jenkins'de tanımlanan kimlik bilgisi ID'si



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
        stage("Build ") {
            steps {
                script {
            dockerImage = docker.build registry + "/" + projectName + ":$BUILD_NUMBER"

                }
            }
        }
                stage("Push Image") {
            steps {
                script {
                    docker.withServer(HARBOR_REGISTRY) {
                        withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'harbor-id', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                            sh "echo ${PASSWORD} | docker -H tcp://127.0.0.1:2376 --config /bitnami/jenkins/home/.docker login harbor.sezer.test:443 -u ${USERNAME} --password-stdin"
                        }
                        sh "docker -H tcp://127.0.0.1:2376 --config /bitnami/jenkins/home/.docker push ${registry}/${projectName}:${IMAGE_TAG}"
                }
            }
        }
    }
}