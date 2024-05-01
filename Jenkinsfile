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
              git branch: 'main', cretentialsId: 'github', url: 'https://github.com/tahaky/jenkinsDemo'
            }
        }
   }
}