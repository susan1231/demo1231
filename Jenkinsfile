tools {
    maven 'Maven3'
}

environment {
    SONARQUBE = 'My SonarQube Server'
}

stages {
    stage('Clone Repository') {
        steps {
            script {
                def repoDir = 'demo1231'
                if (!fileExists(repoDir)) {
                    bat "git clone https://github.com/susan1231/demo1231.git ${repoDir}"
                }
            }
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
                withCredentials([string(credentialsId: 'abc', variable: 'SONAR_TOKEN')]) {
                    withSonarQubeEnv("${SONARQUBE}") {
                        bat "mvn sonar:sonar -Dsonar.login=%SONAR_TOKEN%"
                    }
                }
            }
        }
    }
}
