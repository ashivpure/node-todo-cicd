pipeline {
    agent { label 'Node3-agent' }
    
    stages{
        stage('Code'){
            steps {
                git url: 'https://github.com/ashivpure/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build and Test'){
            steps {
                sh 'docker build . -t ashivpure/node-todo-app:latest' 
            }
        }
        stage('Login and Push Image'){
            steps {
                echo 'logging in to docker hub and pushing image..'
                withCredentials([usernamePassword(credentialsId:'dockerhub', passwordVariable:'dockerHubPassword', usernameVariable:'dockerHubUser')]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push ashivpure/node-todo-app:latest"
                }
            }
        }
        stage('Deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
