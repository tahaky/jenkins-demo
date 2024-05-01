<<<<<<< HEAD
pipeline{
    agent{
        label "jenkins-worker"
    }
    tools{
        jdk 'Java17'
        maven 'Maven3'
    }
    stages{
        stage("Clean Workspace"){
            steps{
                cleanWs()
            }
=======
pipeline {
  agent any
  stages {
    stage('build') {
      post {
        always {
          echo '========always========'
        }

        success {
          echo '========build executed successfully========'
>>>>>>> f307c03695036710a9f44120a77db6ffb692306a
        }

        failure {
          echo '========A execution failed========'
        }

      }
      steps {
        bat 'mvn compile'
      }
    }
<<<<<<< HEAD
    stages{
        stage("Checkout F SCM"){
            steps{
                
            }
=======

    stage('docker image') {
      post {
        always {
          echo '====++++always++++===='
        }

        success {
          echo '====++++docker image executed successfully++++===='
        }

        failure {
          echo '====++++docker image execution failed++++===='
>>>>>>> f307c03695036710a9f44120a77db6ffb692306a
        }

      }
      steps {
        bat "docker build -t ${env.GIT_BRANCH} ."
      }
    }

  }
  post {
    always {
      echo '========always========'
    }

    success {
      echo '========pipeline executed successfully ========'
    }

    failure {
      echo '========pipeline execution failed========'
    }

  }
}