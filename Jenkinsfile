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
                bat 'echo Simulando build'
            }
        }

        stage('Unit tests') {
            steps {
                bat 'echo Simulando unit tests'
                // archiveArtifacts artifacts: 'results/*.xml'
            }
        }

        stage('API Tests') {
            steps {
                echo 'Running API Tests'
                bat 'echo Simulando API tests'
                // archiveArtifacts artifacts: 'results/api/*.xml'
            }
        }

        stage('E2E Tests') {
            steps {
                echo 'Running E2E Tests'
                bat 'echo Simulando E2E tests'
                // archiveArtifacts artifacts: 'results/e2e/*.xml'
            }
        }
    }

    post {
        always {
            // No hay resultados junit porque es simulación
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
