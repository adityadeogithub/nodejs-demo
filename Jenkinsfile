pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('adityadocker13')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/adityadeogithub/nodejs-demo'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t valaxy/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push valaxy/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

