pipeline {
    agent any

    stages {
        stage('Build with Maven') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def imageTag = "java-app:%BUILD_NUMBER%"
                    bat "docker build -t ${imageTag} ."
                }
            }
        }
    }
}
