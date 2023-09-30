pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t huychac03/nginx-jenkins:1.0.0.1 .'
            }
        }
        stage('Login') {
            steps {
                sh 'docker login -u huychac03 -p huychac123'
            }
        }
        stage('Push') {
            steps {
                sh 'docker push huychac03/nginx-jenkins:1.0.0.1'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
