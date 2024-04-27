pipeline{
    agent any
     parameters {
    gitParameter branchFilter: 'origin/(.*)', defaultValue: 'master', name: 'BRANCH', type: 'PT_BRANCH'
   }
    stages{
        stage("build"){
            steps{
               bat 'mvn compile'
            }
        }
        stage("docker image"){
            steps{
                 git branch: "${params.BRANCH}", url: 'https://github.com/jenkinsci/git-parameter-plugin.git'
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}