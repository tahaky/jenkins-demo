pipeline{
    agent{
        label "node"
    }
    stages{
        stage("clonning repository"){
          echo "====++++hello++++===="
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