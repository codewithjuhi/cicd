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
 stage('SonarQube Analysis') {
            steps {
                echo 'Running SonarQube analysis...'

                withSonarQubeEnv('SonarQube') {
                    bat 'mvn sonar:sonar -Dsonar.projectKey=cicd-demo1'
                }
            }
        }
    }
    stage('Test') {
        steps {
            bat 'mvnw.cmd test'
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
        echo 'Build successful!'
    }

    failure {
        echo 'Build failed!'
    }
}

}
