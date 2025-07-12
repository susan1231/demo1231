tools {
    maven 'Maven3'
}

environment {
    SONARQUBE = 'My SonarQube Server'
}

stages {
    stage('Build') {
        steps {
            bat 'dir'
            bat 'mvn clean install'
        }
    }

    stage('SonarQube Analysis') {
        steps {
            withSonarQubeEnv("${SONARQUBE}") {
                bat 'mvn sonar:sonar'
            }
        }
    }
}
