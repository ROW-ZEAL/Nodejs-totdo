pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    def imageName = 'todoapp'
                    def dockerImage = docker.build(imageName, '.')
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    def containerId = docker.image(imageName).run('-p 8001:8001 -d')
                    echo "Docker container started with ID: ${containerId}"
                }
            }
        }
    }

    post {
        always {
            script {
                docker.image(imageName).stop()
                docker.image(imageName).remove()
            }
        }
    }
}
