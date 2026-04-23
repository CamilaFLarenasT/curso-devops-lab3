pipeline {
    agent any

    stages {
        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run tests') {
            steps {
                sh 'npm run test'
            }
        }

        stage('Coverage') {
            steps {
                sh 'npm run test:cov'
            }
        }

        stage('Build app') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Build Docker image') {
            steps {
                sh 'docker build -t curso-devops-lab3:${BUILD_NUMBER} .'
                sh 'docker tag curso-devops-lab3:${BUILD_NUMBER} curso-devops-lab3:latest'
            }
        }

        stage('Deploy Kubernetes') {
            steps {
                sh 'kubectl set image deployment/curso-devops-app curso-devops-container=curso-devops-lab3:${BUILD_NUMBER} -n clarena'
                sh 'kubectl rollout status deployment/curso-devops-app -n clarena'
                sh 'kubectl get pods -n clarena'
            }
        }
    }
}