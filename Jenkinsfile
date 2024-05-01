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
        }
        stage("Checkout F SCM"){
            steps{
              git branch: 'main', credentialsId: 'github', url: 'https://github.com/tahaky/jenkinsDemo'
            }
      }
    stage("Build"){
            steps{
              sh 'mvn clean package'
            }
        }
        stage("Test"){
            steps{
              sh 'mvn test'
            }
        }
}
}