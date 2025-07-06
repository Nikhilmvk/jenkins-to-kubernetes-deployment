pipeline {
    agent any

    tools {
        maven 'Maven3.9.10'
    }

    environment {
        SONAR_TOKEN = credentials('sonar-token')
    }

    stages {
        stage('Build with Maven') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('MySonarQube') {
                    bat "mvn sonar:sonar -Dsonar.projectKey=java-app-pipeline -Dsonar.login=%SONAR_TOKEN%"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t myapp .'
            }
        }

        stage('Trivy Scan') {
            steps {
                bat 'C:\\Tools\\Trivy\\trivy.exe image --scanners vuln --timeout 10m myapp'
            }
        }
    }
}
