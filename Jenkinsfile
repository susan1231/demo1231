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
            bat 'dir'
        }
    }

    stage('Build') {
        steps {
            bat 'mvn clean install'
        }
    }

    stage('SonarQube Analysis') {
        steps {
            withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                withSonarQubeEnv("${SONARQUBE}") {
                    bat "mvn sonar:sonar -Dsonar.login=%SONAR_TOKEN%"
                }
            }
        }
    }
}
