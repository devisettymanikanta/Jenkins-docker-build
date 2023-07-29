pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('mani214-docker')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/devisettymanikanta/Jenkins-docker-build.git']])
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t mani214/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push mani214/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

