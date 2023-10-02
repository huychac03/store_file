pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment {
        CONTAINER_REPOSITORY= "huychac03"
        APPLICATION_NAME= "nginx-jenkins"

        DOCKERHUB_USERNAME = credentials('dockerhub').username
        DOCKERHUB_PASSWORD = credentials('dockerhub').password
        

    }

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t ${CONTAINER_REPOSITORY}/${APPLICATION_NAME}:1.0.0.4 .'
            }
        }
        stage('Login') {
            steps {
                script {
                    // Use the 'dockerhub2' credentials to log in
                    // withCredentials([usernamePassword(
                    //     credentialsId: 'dockerhub',
                    //     usernameVariable: 'DOCKERHUB_USERNAME',
                    //     passwordVariable: 'DOCKERHUB_PASSWORD'
                    // )]) {
                    //     sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
                    // }
                    sh 'docker login -u ${DOCKERHUB_USERNAME} -p ${DOCKERHUB_PASSWORD}'
                }               
            }
        }
        stage('Push') {
            steps {
                sh 'docker push ${CONTAINER_REPOSITORY}/${APPLICATION_NAME}:1.0.0.4'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
