node {
    stage('Clone Repo') {
        git branch: 'react-app', url:'https://github.com/agus-3rd-yoga/a428-cicd-labs.git'
    }
}
pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
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
                 sh 'npm run test'
            }
        }
    }
}
