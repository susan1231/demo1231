pipeline {
    agent any

    environment {
        SONARQUBE = 'My SonarQube Server'
    }

    stages {
        stage('Setup Maven') {
            steps {
                script {
                    // Set up Maven tool installation named 'Maven3'
                    env.MAVEN_HOME = tool 'Maven3'
                    // Add Maven bin to PATH
                    env.PATH = "${env.MAVEN_HOME}\\bin;${env.PATH}"
                }
            }
        }

        stage('Clone Repository') {
            steps {
                // Clone the repository from GitHub using the main branch
                git branch: 'main', url: 'https://github.com/susan1231/demo1231.git'  // Replace with your repo URL
                
                // List files in the repository for debugging purposes
                bat 'dir'
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
