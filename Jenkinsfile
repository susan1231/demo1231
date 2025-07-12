pipeline {
    agent any

    tools {
        maven 'Maven3'  // Maven tool defined in Jenkins' global tools configuration
    }

    environment {
        SONARQUBE = 'My SonarQube Server'  // Name of your SonarQube server as configured in Jenkins
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the repository from GitHub using the main branch
              bat 'git clone https://github.com/susan1231/demo1231.git'// Replace with your repo URL
                
                // List files in the repository for debugging purposes
                bat 'dir'
            }
        }

        stage('Build') {
            steps {
                // Run Maven clean install in the root directory (where pom.xml is)
                bat 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Run SonarQube analysis in the root directory
                withSonarQubeEnv("${SONARQUBE}") {  
                    bat 'mvn sonar:sonar'
                }
            }
        }
    }
}
