pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t pulkit-webapp:${BUILD_NUMBER} .'
            }
        }

        stage('Load Image into Minikube') {
            steps {
                sh 'minikube image load pulkit-webapp:${BUILD_NUMBER}'
            }
        }

        stage('Deploy with Helm') {
            steps {
                sh '''
                helm upgrade --install devops-webapp ./helm/webapp \
                  --set image.repository=pulkit-webapp \
                  --set image.tag=${BUILD_NUMBER}
                '''
            }
        }
    }
}
