pipeline {
    agent {
        docker {
            image 'node:lts-buster-slim'
            args '-p 3003:3003'
        }
    }
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
        stage('Deploy') {
            steps {
                sh 'npm run build'
                sh 'JENKINS_NODE_COOKIE=dontKillMe nohup npx --yes serve -s build -l 3003 > serve.log 2>&1 &'
                sh 'sleep 5 && curl -sf http://localhost:3003 > /dev/null && echo "Deploy OK: app up di port 3003 (host: 3003)"'
            }
        }
    }
}
