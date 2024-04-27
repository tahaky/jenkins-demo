pipeline{
    agent any
     parameters {
      gitParameter branchFilter: 'main/(.*)', defaultValue: 'master', name: 'BRANCH', type: 'PT_BRANCH'
   }
    stages{
        stage("build"){
            steps{
               bat "echo ${params.BRANCH}"
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