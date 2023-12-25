pipeline {
    agent {
        docker {
            image 'node'
            args '-p 3000:3000'
            alwaysPull false
            reuseNode true
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
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Manual Approval') { 
            steps {
                input message: 'Lanjut ke tahap deploy? \
                    (Klik "Proceed" untuk melanjutkan eksekusi pipeline ke tahap Deploy)'
            }
        }
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh'
                sh 'sleep 60'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
