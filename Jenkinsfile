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
