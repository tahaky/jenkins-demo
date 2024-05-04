pipeline {
    agent {
        label "worker-node"
    }
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
    stages {
        stage("Clean Workspace") {
            steps {
                cleanWs()
            }
        }
        stage("Checkout F SCM") {
            steps {
                git branch: 'main', credentialsId: 'jenkins-github', url: 'https://github.com/tahaky/jenkinsDemo'
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
       stage("Sonarqube Analysis") {
            steps {
                withSonarQubeEnv(credentialsId:'jenkins-sonarqube-token')
                sh 'mvn sonar:sonar'
            }

        }
    }
}
