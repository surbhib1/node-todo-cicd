pipeline{
    agent { 
        label 'dev-agent'     
    }
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/surbhib1/node-todo-cicd.git', branch: 'master'
            }
     }
     stage('Code Build and Test'){
            steps{
                sh 'docker build . -t surbhib1/node-todo-app-cicd:latest'
            }
     }
     stage('Login and Push Image'){
            steps{
                echo 'logging in to docker hub and pushing image'
                withCredentials([usernamePassword(credentialsId:'dockerHub', passwordVariable:'dockerHubpassword', usernameVariable:'dockerHubuser')]) {
                                  sh "docker login -u ${env.dockerHubuser} -p ${env.dockerHubpassword}"
                                  sh "docker push ${env.dockerHubuser}/node-todo-app-cicd:latest"
                      
                }
            }
     }
     stage('Code Deploy'){
            steps{
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
    
}
