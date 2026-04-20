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
                sh 'newman run collections/genkins-test.postman_collection.json -d collections/genkins-test.postman_collection-variables.json --reporters cli'
            }
        }
    }

    post {
        always {
            echo "Pipeline finished."
        }
        failure {
            echo "API tests failed! Check the logs."
        }
    }
}
