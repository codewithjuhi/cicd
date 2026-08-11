pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvnw.cmd clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvnw.cmd test'
            }
        }

       stage('SonarQube Analysis') {
           steps {
               withSonarQubeEnv('SonarQube') {
                   bat 'mvnw.cmd clean verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=cicd-demo1 -Dsonar.projectName=cicd-demo1'
               }
           }
       }

        stage('Verify') {
            steps {
                bat 'dir target'
            }
        }
    }

    post {
        success {
            echo 'Build and SonarQube analysis successful!'
        }

        failure {
            echo 'Build or SonarQube analysis failed!'
        }
    }
}