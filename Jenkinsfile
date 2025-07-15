pipeline {
    agent any
tools {
    maven 'Maven3' // Ensure this name matches Global Tool Configuration
}

environment {
    SONARQUBE = 'My SonarQube Server' // Must match the name in Jenkins → Configure System
}

stages {

    stage('Clean Workspace') {
        steps {
            cleanWs() // Clean workspace to avoid git clone conflicts
        }
    }

    stage('Clone Repository') {
        steps {
            // Delete folder if it already exists (extra safety)
            bat 'if exist demo1231 rmdir /s /q demo1231'
            bat 'git clone https://github.com/susan1231/demo1231.git'
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
                withCredentials([string(credentialsId: '842aacf4-1ada-4c22-86bc-d4693eef4dbd', variable: 'SONAR_TOKEN')]) {
                    withSonarQubeEnv("${SONARQUBE}") {
                        bat 'mvn sonar:sonar -Dsonar.login=%SONAR_TOKEN%'
                    }
                }
            }
        }
    }
}

}
