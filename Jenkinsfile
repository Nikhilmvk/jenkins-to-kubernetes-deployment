pipeline {
    agent any

    tools {
        maven 'Maven3.9.10'   // 👈 Match the name from Global Tool Config
    }

    stages {
        stage('Build with Maven') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t myapp .'
            }
        }
    }
}
