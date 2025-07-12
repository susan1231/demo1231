tools {
    maven 'Maven3'
}

environment {
    SONARQUBE = 'My SonarQube Server'
}

stages {
    stage('Clone Repository') {
        steps {
            git url: 'https://github.com/susan1231/demo1231.git', branch: 'main'
        }
    }

    stage('Build') {
        steps {
            bat 'mvn clean install'
        }
    }

    stage('SonarQube Analysis') {
        steps {
            withCredentials([string(credentialsId: '943dd257-9fe0-4dc0-969e-9f59ccc9d8f4', variable: 'SONAR_TOKEN')]) {
                withSonarQubeEnv("${SONARQUBE}") {
                    bat "mvn sonar:sonar -Dsonar.login=%SONAR_TOKEN%"
                }
            }
        }
    }
}
