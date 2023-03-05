pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/yogendra-kokamkar/todo-node-cicd.git', branch:'K8s-CICD'
      }
    }
    
      stage("Build image") {
            steps {
                script {
                    myapp = docker.build("yogendrakokamkar/todonodekube:${env.BUILD_ID}")
                }
            }
        }
    
      stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

    
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "todokube.yml", kubeconfigId: "kubernetes")
        }
      }
    }

  }

}
