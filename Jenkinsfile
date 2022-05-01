pipeline {
    environment {
    dockerImageName = "gwin300/node-app"
    dockerImage = ""
}
    agent any
    stages {
        
        stage('Example') {
            steps {
                echo 'Hello World'
            }
        }
        
          stage('build') {
             steps {
                script {
                    dockerImage = docker.build dockerImageName
                }
            }
        }
        
    }
}
