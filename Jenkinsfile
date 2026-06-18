pipeline {
    agent any
    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64/'
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }
    stages {
        stage('GIT') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/tnnebras/3ACC_Nouioui.git'
            }
        }
        stage('MAVEN') {
            steps {
                sh "mvn clean package -DskipTests"
            }
        }
        stage('SONARQUBE') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh "mvn sonar:sonar"
                }
            }
        }
    }
}