pipeline{
        agent {label 'prod-agent'}
            stages{
                stage('Code'){
                    steps{
                        git url: 'https://github.com/SantoshMorla/node-todo-cicd.git',branch: 'master'
                    }
                }
                stage('Build and Test'){
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
                }
                stage('Deploying'){
                    steps{
                        // sh 'docker run -d -p 8000:8000 devsantosh03/node-todo-app:latest'
                        sh 'docker compose down && docker compose up -d' 
                    }
                }
            }    
        }
