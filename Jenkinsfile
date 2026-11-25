pipeline {
    agent any

    triggers {
        pollSCM('H/2 * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    sudo -H -u aditya kubectl apply -f kubernetes/deployment.yaml
                    sudo -H -u aditya kubectl apply -f kubernetes/service.yaml
                    sudo -H -u aditya kubectl rollout status deployment/devops-lab2
                '''
            }
        }

        stage('Verify') {
            steps {
                sh '''
                    sudo -H -u aditya kubectl get deployments
                    sudo -H -u aditya kubectl get pods
                    sudo -H -u aditya kubectl get services
                    sudo -H -u aditya kubectl get deployment devops-lab2 -o jsonpath='{.spec.template.spec.containers[0].image}'
                '''
            }
        }
    }

    post {
        success {
            echo 'Continuous deployment completed successfully!'
        }
        failure {
            echo 'Continuous deployment failed.'
        }
    }
}
