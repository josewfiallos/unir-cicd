pipeline {
    agent any

    stages {
        stage('Source') {
            steps {
                git 'https://github.com/josewfiallos/unir-cicd.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building stage!'
                bat 'make build'
            }
        }

        stage('Unit tests') {
            steps {
                bat 'make test-unit'
                archiveArtifacts artifacts: 'results/*.xml'
            }
        }

        stage('API Tests') {
            steps {
                echo 'Running API Tests'
                bat 'make test-api'
                archiveArtifacts artifacts: 'results/api/*.xml'
            }
        }

        stage('E2E Tests') {
            steps {
                echo 'Running E2E Tests'
                bat 'make test-e2e'
                archiveArtifacts artifacts: 'results/e2e/*.xml'
            }
        }
    }

    post {
        always {
            junit 'results/**/*.xml'
            cleanWs()
        }
        failure {
            echo "Sending failure notification email"
            echo "Job: ${env.JOB_NAME} - Build: ${env.BUILD_NUMBER}"
            // Ejemplo: mail to: 'destinatario@dominio.com', subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}", body: "Verificar el pipeline"
        }
    }
}
