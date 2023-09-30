pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment {
        DOCKERHUB_CREDENTIAL_ID = credentials('dockerhub-pass')
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t huychac03/nginx-jenkins:1.0.0.1 .'
            }
        }
        stage('Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: DOCKERHUB_CREDENTIAL_ID, usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'docker login -u $USERNAME -p $PASSWORD'
                }
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
