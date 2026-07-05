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
                sh 'docker build -t bishorana1/devops-mastery-pipeline:${BUILD_ID} .'
                sh 'docker tag bishorana1/devops-mastery-pipeline:${BUILD_ID} bishorana1/devops-mastery-pipeline:latest'
            }
        }
        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker push bishorana1/devops-mastery-pipeline:${BUILD_ID}'
                    sh 'docker push bishorana1/devops-mastery-pipeline:latest'
                }
            }
        }
    }
}
