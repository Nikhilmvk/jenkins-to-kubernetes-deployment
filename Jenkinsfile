pipeline {
    agent any

    tools {
        maven 'Maven3.9.10'  // Make sure this is correctly configured in Jenkins Global Tool Configuration
    }

    environment {
        SONAR_TOKEN = credentials('sonar-token') // ID from Jenkins > Manage Credentials
    }

    stages {
        stage('Build with Maven') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('MySonarQube') { // Matches Jenkins > Configure System > SonarQube name
                    bat "mvn sonar:sonar -Dsonar.projectKey=java-app-pipeline -Dsonar.login=%SONAR_TOKEN%"
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
