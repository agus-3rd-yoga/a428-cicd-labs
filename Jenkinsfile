node {
    stage('Clone Repo') {
        git branch: 'main', url:'https://github.com/agus-3rd-yoga/weather-app.git'
    }
}

pipeline {
    agent {
        docker {
            image 'node:16-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test --passWithNoTests'
            }
        }
        stage('Manual Approval') {
            steps {
                script {
                    sh 'sleep 1'
                    input message: 'Lanjutkan ke tahap Deploy? (Click "Proceed" to continue)'
                }
            }
        }
        stage('Deploy') { 
            steps {
                sh  './jenkins/scripts/deliver.sh'
                sh  'npm install --save gh-pages'
                sh  'sleep 60'
                sh  './jenkins/scripts/kill.sh'
            }
        }
    }
}