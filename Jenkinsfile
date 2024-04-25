pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Use SSH credentials for Git authentication
                git credentialsId: 'Docker', url: 'https://github.com/Musaele/CI_CD.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('musaele1/ci-cd:latest')
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub_credentials') {
                        docker.image('musaele1/ci-cd:latest').push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }

        stage('Run Container') {
            steps {
                sh 'kubectl get pods'
                // Run additional commands as needed to verify deployment and run container
            }
        }
    }
}