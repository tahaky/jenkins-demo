pipeline{
    agent any
     parameters {
      gitParameter branchFilter: 'main/(.*)', defaultValue: 'main', name: 'BRANCH', type: 'PT_BRANCH'
   }
    stages{
        stage("build"){
            steps{
               sh "mvn install"
               echo "---Project dependency's succesfuly installed---"
               sh "mvn test"
               echo "---Project passed all of the test---"
               sh "docker build -t demo-${params.BRANCH} ."
                     post{
                success{
                    echo "---build stage executed successfully---"
                }
                failure{
                    echo "---build stage execution failed---"
                }
        
            }
            }
        }
        stage("A"){
            steps{
                echo "====++++executing A++++===="
            }
            post{
                always{
                    echo "====++++always++++===="
                }
                success{
                    echo "====++++A executed successfully++++===="
                }
                failure{
                    echo "====++++A execution failed++++===="
                }
        
            }
        }
    }
    post{
        success{
            echo "---pipeline executed successfully---"
        }
        failure{
            echo "---pipeline execution failed---"
        }
    }
}