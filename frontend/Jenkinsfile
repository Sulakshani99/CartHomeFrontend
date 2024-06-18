pipeline {
    agent any 
   
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/Sulakshani99/4035-Kumari'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t sulakshani99/nodeapp-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
               withCredentials([string(credentialsId: 'test-dockerhubpassword', variable: 'test-dockerhubpass')]) {
                script {
                        bat'docker login -u sulakshani99 -p ${{test-dockerhubpass}}'
                }
            }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push sulakshani99/nodeapp-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}