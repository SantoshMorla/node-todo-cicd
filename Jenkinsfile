pipeline{
        agent {label 'Dev-Django'}
            stages{
                stage('Code'){
                    steps{
                        git url: 'https://github.com/SantoshMorla/django-todo-cicd.git',branch: 'develop'
                    }
                }
                
                stage('Build and Test'){
                    steps {
                        sh 'docker build . -t django-app-latest'
                    }
                }
                
                stage('Deploying'){
                    steps{
                      sh 'docker-compose down && docker-compose up -d' 
                    }
                }
                 
    
            }    
        }
