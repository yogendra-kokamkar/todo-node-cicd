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
                sh 'sudo docker build . -t yogendrakokamkar/todonode:latest'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'Docker', passwordVariable: 'DockerPassword', usernameVariable: 'DockerUser')]) {
        	     sh "sudo docker login -u ${env.DockerUser} -p ${env.DockerPassword}"
                 sh 'sudo docker push yogendrakokamkar/todonode:latest'
                }
            }
        }
        stage('Deploy'){
            steps{
                sh "sudo docker-compose down && docker-compose up -d"
            }
        }
    }
}
