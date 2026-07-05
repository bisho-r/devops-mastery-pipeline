pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github-token', url: 'https://github.com/bisho-r/devops-mastery-pipeline.git'
            }
        }
        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    try {
                        sh 'docker build -t bishorana1/devops-mastery-pipeline:latest .'
                    } catch (Exception e) {
                        echo "Docker build skipped - Docker not available in Jenkins"
                    }
                }
            }
        }
    }
}
