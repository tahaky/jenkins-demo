pipeline{
    agent any
     parameters {
      gitParameter branchFilter: 'main/(.*)', defaultValue: 'main', name: 'BRANCH', type: 'PT_BRANCH'
   }
    stages{
        stage("build"){
            steps{
               bat "mvn install"
               echo "---Project dependency's succesfuly installed---"
               bat "mvn test"
               echo "---Project passed all of the test---"
               bat "docker build -t demo-${params.BRANCH} ."
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