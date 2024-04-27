pipeline{
    agent any
    stages{
        stage("build"){
            steps{
               bat 'mvn compile'
            }
        }
        stage("docker image"){
            steps{
                  bat  "docker build -t ${env.BRANCH_NAME} ."
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