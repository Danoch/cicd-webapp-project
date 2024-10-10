pipeline {
    agent any
    
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-credentials-id')
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Checkout the code from GitHub
                git 'https://github.com/Danoch/cicd-webapp-project.git'
            }
        }
        
        stage('Build Docker Images') {
            steps {
                script {
                    // Build frontend Docker image
                    sh 'docker build -t react-frontend ./frontend'
                    
                    // Build backend Docker image
                    sh 'docker build -t node-backend ./backend'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                    
                    // Tag and push the frontend Docker image
                    sh 'docker tag react-frontend your-dockerhub-username/react-frontend:latest'
                    sh 'docker push your-dockerhub-username/react-frontend:latest'
                    
                    // Tag and push the backend Docker image
                    sh 'docker tag node-backend your-dockerhub-username/node-backend:latest'
                    sh 'docker push your-dockerhub-username/node-backend:latest'
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                script {
                    // Deployment logic to AWS EKS using kubectl
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed!'
        }
    }
}
