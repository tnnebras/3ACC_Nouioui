pipeline {
    agent any
    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64/'
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
        DOCKER_IMAGE = 'tnnebras/nouioui_3acc_student-management:1.0.0'
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
        stage('DOCKER BUILD') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }
        stage('DOCKER PUSH') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "echo ${DOCKER_PASS} | docker login -u ${DOCKER_USER} --password-stdin"
                    sh "docker push ${DOCKER_IMAGE}"
                }
            }
        }
    }
}