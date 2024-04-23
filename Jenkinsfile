pipeline {
    agent any 
   
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/Pubudu-Piyankara/node.git'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t pubudu999/test-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'docPass', variable: 'dockerPassword')]) {
    // some block
               bat'docker login -u pubudu999 -p ${docPass }'
}
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push pubudu999/test-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}