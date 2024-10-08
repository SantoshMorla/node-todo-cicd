pipeline {
        agent{label 'prod-agent'}
            stages{
                stage('Code'){
                    steps {
                        git url: 'https://github.com/SantoshMorla/node-todo-cicd.git', branch: 'master'
                    }
                }
                stage('Build and Test'){
                        when{
                                environment name: 'env-prod', value: 'Tanew@2686' 
                            }
                    steps {
                        sh 'docker build . -t devsantosh03/node-todo-app:latest'
                    }
                }
                stage('Logging  and Push'){
                    steps {
                        withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable:'dockerhubPassword',usernameVariable:'userName')]){
                        sh "docker login -u ${env.userName} -p ${env.dockerhubPassword}"
                        sh "docker push  devsantosh03/node-todo-app:latest"
                        }
                    }
                     post{
                      always {
                                  echo 'This will always run, no matter what the result of the pipeline is.'
                        }
                         success {
                             echo 'This will run if the pipeline is successful.'
                       }
                        failure {
                          echo 'This will run if the pipeline fails.'
                                }
                     }      
                }
                stage('Deploying'){
                   
                    steps{
                        // sh 'docker run -d -p 8000:8000 devsantosh03/node-todo-app:latest'
                        sh 'docker compose down && docker compose up -d' 
                    }
                
                post{
                      always {
                                  echo 'This will always run, no matter what the result of the pipeline is.'
                        }
                         success {
                             echo 'This will run if the pipeline is successful.'
                       }
                        failure {
                            echo 'This will run if the pipeline fails.'
                                }
                        unstable {
                             echo 'This will run if the pipeline is unstable.'
                        }
                        changed {
                             echo 'This will run if the pipeline result changes compared to the previous run.'
                         }
                    } 
                 }       
          
             }
}
