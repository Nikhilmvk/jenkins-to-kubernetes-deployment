pipeline {
    agent any

    tools {
        maven 'Maven3.9.10'  // Make sure this is correctly configured in Jenkins Global Tool Configuration
    }

    environment {
        SONAR_TOKEN = credentials('sonar-token') // 👈 This must match the ID of the token in Jenkins Credentials
    }

    stages {
        stage('Build with Maven') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('MySonarQube') { // 👈 Must match Jenkins SonarQube server name
                    bat "mvn sonar:sonar -Dsonar.projectKey=java-app-pipeline -Dsonar.login=${sonar-token}"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t myapp .'
            }
        }
    }
}
