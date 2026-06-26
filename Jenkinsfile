pipeline {
    agent any

    parameters {
        string(name: 'IMAGE_TAG', defaultValue: 'v2', description: 'Docker image tag to deploy')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Helm Deploy') {
            steps {
                sh '''
                    helm upgrade --install helm-demo ./helm-demo-chart \
                    --set image.tag=${IMAGE_TAG}
                '''
            }
        }

        stage('Verify') {
            steps {
                sh '''
                    kubectl get pods
                    kubectl get svc
                    helm list
                '''
            }
        }
    }
}
