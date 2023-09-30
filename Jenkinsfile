pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment {
        DOCKERHUB_USERNAME = credentials('dockerhub-pass_USR')
        DOCKERHUB_PASSWORD = credentials('dockerhub-pass_PSW').toString()
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t huychac03/nginx-jenkins:1.0.0.1 .'
            }
        }
        stage('Login') {
            steps {
                // sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
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
