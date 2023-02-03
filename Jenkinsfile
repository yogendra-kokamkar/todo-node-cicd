pipeline {
    agent {label 'node-agent'}
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/yogendra-kokamkar/todo-node-cicd.git', branch: 'main' 
            }
        }
        stage('Build and Test'){
            steps{
                sh 'sudo docker build . -t yogendrakokamkar/todonode:v2'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'Docker', passwordVariable: 'DockerPassword', usernameVariable: 'DockerUser')]) {
        	     sh "sudo docker login -u ${env.DockerUser} -p ${env.DockerPassword}"
                 sh 'sudo docker push yogendrakokamkar/todonode:v2'
                }
            }
        }
        stage('Deploy'){
            steps{
                sh "sudo docker-compose down && sudo docker-compose up -d"
            }
        }
    }
}
