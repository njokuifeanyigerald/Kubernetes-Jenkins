pipeline{
    agent{
        label "master"
    }
    stages{
        stage("github checkout"){
            steps{
                echo "========executing github checkout========"
                git credentialsId: 'github-access', url: 'https://github.com/njokuifeanyigerald/Kubernetes-Jenkins.git'
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========github checkout executed successfully========"
                }
                failure{
                    echo "========github checkout execution failed========"
                }
            }
        }
      stage("k8s"){
          steps{
              echo "====++++executing k8s++++===="
              script {
                kubernetesDeploy(configs: "flask.yaml", kubeconfigId: "myKubeConfig") 
                
              }
          }
          post{
              always{
                  echo "====++++always++++===="
              }
              success{
                  echo "====++++k8s executed successfully++++===="
              }
              failure{
                  echo "====++++k8s execution failed++++===="
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