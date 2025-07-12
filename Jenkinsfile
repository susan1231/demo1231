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
                // Checking if the directory exists, if not then clone it
                script {
                    def repoDir = 'demo1231'
                    if (!fileExists(repoDir)) {
                        bat "git clone https://github.com/susan1231/demo1231.git ${repoDir}"
                    }
                }
                dir('demo1231') {
                    bat 'dir'  // List the directory to verify the clone
                }
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

       stage('SonarQube Analysis') {
            steps {
                dir('demo1231') {
                    withSonarQubeEnv("${SONARQUBE}") {  // Run SonarQube analysis
                        bat 'mvn sonar:sonar'
                    }
                }
            }
        }
    }
}
