node {
    docker.image('python:3.11.4-slim').inside('-u 0:0') {
        stage('Checkout') {
            checkout scm
        }

        stage('Install Dependencies') {
            sh 'apt-get update && apt-get install -y binutils'
            sh 'pip install pytest pyinstaller'
        }

        stage('Test') {
            sh 'pytest --junitxml=reports/results.xml'
            junit 'reports/results.xml'
        }

        stage('Build') {
            sh 'pyinstaller --onefile --name react-app app/main.py'
        }

        stage('Manual Approval') {
            steps {
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
            }
        }

        stage('Deploy') {
            steps {
                sh 'chmod +x dist/react-app'
                sh './dist/react-app &'
                sleep 60
                sh 'pkill -f react-app || true'
            }
        }
    }
}