pipeline {
    agent any
    tools {nodejs "NODEJS"}
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
    post {
    success {
        echo 'The build was successful please merge'
    }
    failure {
        echo 'The build failed'
    }
    always {
        cleanWs()
        }
    }
}
