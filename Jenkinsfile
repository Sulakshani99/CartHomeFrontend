// pipeline {
//     agent any 
   
    
//     stages { 
//         stage('SCM Checkout') {
//             steps {
//                 retry(3) {
//                     git branch: 'main', url: 'https://github.com/Sulakshani99/CartHomeFrontend'
//                 }
//             }
//         }
//         stage('Build Docker Image') {
//             steps {  
//                 bat 'docker build -t sulakshani99/carthome-frontend:%BUILD_NUMBER% .'
//             }
//         }
//         stage('Login to Docker Hub') {
//             steps {
//                withCredentials([string(credentialsId: 'frontend-dockerhubpassword', variable: 'frontend-dockerhub')]) 
//                {
//                 script {
//                         bat'docker login -u sulakshani99 -p ${{frontend-dockerhub}}'
//                 }
//                 }
//             }
//         }
//         stage('Push Image') {
//             steps {
//                 bat 'docker push sulakshani99/carthome-frontend:%BUILD_NUMBER%'
//             }
//         }
//     }
//     post {
//         always {
//             bat 'docker logout'
//         }
//     }
// }






pipeline {
    agent any 
   
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(10) {
                    git branch: 'main', url: 'https://github.com/Sulakshani99/CartHomeFrontend'
                }
            }
        }
        stage('Build Docker Images') {
            steps {
                script {
                    bat 'docker build -t sulakshani99/carthome-frontend:%BUILD_NUMBER% frontend'
                    // bat 'docker build -t sulakshani99/carthome-backend:%BUILD_NUMBER% backend'

                }
            }
        }
        stage('Login to Docker Hub') {
    steps {
        withCredentials([string(credentialsId: 'frontend-dockerhubpassword', variable: 'frontend-dockerhub')]) {
            bat "docker login -u sulakshani99 -p ${frontend-dockerhub}"
        }
    }
}

        stage('Deploy with Docker Compose') {
            steps {
                script {
                    bat 'docker-compose up -d'
                }
            }
        }

    }
    post {
        always {
            bat 'docker logout'
        }
    }
}