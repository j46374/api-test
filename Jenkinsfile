pipeline {
    agent any

    environment {
        // Define environment variables here
        PROJECT_NAME = "My-API-Tests"
    }

    stages {
        stage('Initialize') {
            steps {
                echo "Starting ${env.PROJECT_NAME}..."
                sh 'node --version'
                sh 'newman --version'
            }
        }

        stage('Checkout') {
            steps {
                // This checks out code from the repo linked to the Jenkins job
                checkout scm
            }
        }

        stage('Run API Tests') {
            steps {
                // Running Newman against your collection in the repo
                withCredentials([string(credentialsId: 'API_PASSWORD', variable: 'API_PASSWORD')]) {
                     sh "newman run collections/genkins-test.postman_collection.json --env-var password=${API_PASSWORD} -d collections/genkins-test.postman_collection-variables.json --reporters cli,htmlextra --reporter-htmlextra-export reports/report.html"
                 }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'reports/*.html', fingerprint: true
            echo "Pipeline finished."
        }
        failure {
            echo "API tests failed! Check the logs."
        }
    }
}
