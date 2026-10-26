pipeline {
    agent {
        docker {
            image 'node:lts-buster-slim'
            args '-p 3003:3003'
        }
    }
    environment {
        CI = 'true'
        HOME = '.'
        NODE_OPTIONS = '--openssl-legacy-provider'
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
    }
}
