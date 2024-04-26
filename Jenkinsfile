pipeline{
    agent{
        label "node"
    }
    stages{
        stage("clon"){
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