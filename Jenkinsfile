pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven'
    }

    stages {

       stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/shubhamkelaskar04/Jenkins-CI-CD.git'
            }
       }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'mvn test'
            }
        }

        stage('JUnit Report') {
            steps {
                junit '**/target/surefire-reports/*.xml'
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                if not exist C:\\deploy mkdir C:\\deploy
                copy target\\jenkins-demo-1.0.jar C:\\deploy
                '''
            }
        }
    }
}
