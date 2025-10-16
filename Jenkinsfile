node {
    docker.image('python:3.11.4-slim').inside {
        stage('Checkout') {
            checkout scm
        }

        stage('Build') {
            sh 'pip install pytest pyinstaller'
        }

        stage('Test') {
            sh 'pytest --junitxml=reports/results.xml'
            junit 'reports/results.xml'
        }
    }
}