pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    environment {
        SONARQUBE = 'My SonarQube Server'
    }

    stages {
        stage('Clone Repository') {
            steps {
                bat 'git clone https://github.com/susan1231/demo1231.git'
                dir('demo1231') {
                    bat 'dir'
                }
            }
        }

        stage('Build') {
            steps {
                dir('demo1231') {
                    bat 'mvn clean install'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                dir('demo1231') {
                    withSonarQubeEnv("${SONARQUBE}") {
                        bat 'mvn sonar:sonar'
                    }
                }
            }
        }
    }
}
