pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment {
        DOCKERHUB_CREDENTIAL_ID = credentials('dockerhub')
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t huychac03/nginx-jenkins:1.0.0.0 .'
            }
        }
        stage('Login') {
            steps {
                withDockerRegistry([credentialsId: DOCKERHUB_CREDENTIAL_ID, url: "https://index.docker.io/v1/"]){
                    
                }
            }
        }
        stage('Push') {
            steps {
                sh 'docker push huychac03/nginx-jenkins:1.0.0.0'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
