pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('valaxy-dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps {
                git 'https://github.com/ravdy/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                bat 'docker build -t valaxy/nodeapp:%BUILD_NUMBER% .'
            }
        }
        
        stage('Login to Docker Hub') {
            steps {
                bat 'echo %DOCKERHUB_CREDENTIALS_PSW% | docker login -u %DOCKERHUB_CREDENTIALS_USR% --password-stdin'
            }
        }
        
        stage('Push Image') {
            steps {
                bat 'docker push valaxy/nodeapp:%BUILD_NUMBER%'
            }
        }
    }
    
    post {
        always {
            bat 'docker logout'
        }
    }
}
