pipeline {
    agent any
    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64/'
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }
    stages {
        stage('MAVEN') {
            steps {
                sh "mvn -version"
                sh "mvn clean package -DskipTests"
            }
        }
    }
}