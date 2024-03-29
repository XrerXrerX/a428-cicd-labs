pipeline {
    agent {
        docker {
            image 'node:lts-buster-slim'
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
                sh './jenkins/scripts/test.sh' 
            }
        }
        stage('deploy') { 
            steps {
                input message: 'ingin lanjut deploy ?? (Klik "Proceed" untuk deploy)' 
                sh './jenkins/scripts/deliver.sh' 
            }
        }
        stage('deliver') { 
            steps {
                script {
                    sleep(time: 60, unit: 'SECONDS')
                }
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}