pipeline{
    // agent any 
    // or
    agent{
        label "master"
    }
    stages{
        stage("clean workspace"){
            steps{
                cleanWs()
            }
            post{
                success{
                    echo "========clean workspace executed successfully========"
                }
                failure{
                    echo "========clean workspace execution failed========"
                }
            }
        }
        stage("github access"){
            steps{
                echo "========executing github access========"
                git credentialsId: 'github-access', url: 'https://github.com/njokuifeanyigerald/Kubernetes-Jenkins.git'
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========github access executed successfully========"
                }
                failure{
                    echo "========github access execution failed========"
                }
            }
        }
        stage("build"){
          steps{
              echo "====++++executing k8s++++===="
              script {
               kubeconfig(credentialsId: 'myKubeConfig', serverUrl: 'https://192.168.59.101:8443') {
                    sh 'kubectl get nodes'
                    sh 'kubectl apply -f flask.yaml'
                    sh 'kubectl get all'
                }
                                
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

        stage("test"){
            steps{
                echo "====++++executing test++++===="
                script {
                    kubeconfig(credentialsId: 'myKubeConfig', serverUrl: 'https://192.168.59.101:8443') {
                            sh 'kubectl get nodes'
                            sh 'kubectl delete -f flask.yaml'
                            sh 'kubectl get all'
                        }               
                }
            }
            post{
                always{
                    echo "====++++always++++===="
                }
                success{
                    echo "====++++test executed successfully++++===="
                }
                failure{
                    echo "====++++test execution failed++++===="
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