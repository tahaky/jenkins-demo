pipeline{
    agent any
    stages{
        stage("build"){
            steps{
               bat 'mvn compile'
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========build executed successfully========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
        stage("docker image"){
            steps{
                  bat  "docker build -t ${env.GIT_BRANCH} ."
            }
            post{
                always{
                    echo "====++++always++++===="
                }
                success{
                    echo "====++++docker image executed successfully++++===="
                }
                failure{
                    echo "====++++docker image execution failed++++===="
                }
        
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