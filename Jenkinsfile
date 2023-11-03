pipeline{
    agent {label 'dev'}
    stages{
        stage('code'){
            steps{
                git url: 'https://github.com/ashivpure/node-todo-cicd.git',branch:'master'
            }
        }
         stage('Build and test'){
            steps{
                sh 'docker build . -t ashivpure/node-todo-app:latest'
                echo "Builing and testing"
            }
        }
        stage('login and push image'){
            steps{
                echo "loging and push image"
                withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable:'dockerhubPassword',usernameVariable:'dockerhubUser')]){
                    sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPassword}"
                    sh "docker push ashivpure/node-todo-app:latest"
                }
            }
        }
         stage('deploy'){
            steps{
                sh 'docker-compose down && docker-compose up -d'
                echo "deploying code.."
            }
        }
         stage('last'){
            steps{
                echo "finally done"
            }
        }
    }
}
