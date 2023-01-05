pipeline {
    agent any
    stages {
        stage("verify tooling") {
            steps {
              sh '''
                docker info
                docker version
                docker compose version
                curl --version
              '''
            }
        }
        stage('start container'){
            steps{
                sh 'docker compose up -d --no-color --wait'
                sh 'docker compose ps'
            }
        }
        stage('Run tests against the container') {
            steps {
                sh 'curl http://localhost:3000/param?query=demo | jq'
            }
        }
    }
    post {
        always {
            sh 'docker ps'
            sh 'docker images'
            sh 'docker volume ls'
        }
    }

}