pipeline {
    agent any

    tools {
        maven 'Maven3.9.10'  // Make sure this name exactly matches Global Tool Configuration
    }

    environment {
        SONARQUBE_ENV = 'MySonarQube'  // Match this with Jenkins > Configure System > SonarQube server name
    }

    stages {
        stage('Build with Maven') {
            steps {
                script {
                    bat 'mvn clean package'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv("${env.SONARQUBE_ENV}") {
                        bat 'mvn sonar:sonar'
                    }
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    bat 'docker build -t myapp .'
                }
            }
        }
    }
}
