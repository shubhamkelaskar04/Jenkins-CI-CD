pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/shubhamkelaskar04/Jenkins-CI-CD.git'
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
                bat 'mkdir C:\\deploy'
                bat 'copy test.txt C:\\deploy'
            }
        }

    }
}
