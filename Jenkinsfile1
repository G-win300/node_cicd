pipeline {
  environment {
    dockerImageName = "gwin300/node-app"
    dockerImage = ""
}
    agent any
        
        stage('build') {
            steps {
                script {
                    dockerImage = docker.build dockerImageName
                }
            }
        }
        
        stage('push docker image') {
            environment {
                registryCredentials = "docker"
                        }
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com/repository/docker/gwin300/node-app', registryCredentials)
                    dockerImage.push("latest")
                }
            }
        }
        
        stage('kubernetes deploy') {
            steps {
                script {
                    kubernetesDeploy(configs: "deployment-service.yaml", kubeconfigId: "kubernetes")
                }
            }
    }
}
}
