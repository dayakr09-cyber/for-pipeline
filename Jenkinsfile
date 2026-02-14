pipeline {
    agent any

    parameters {
        choice(name: 'ENV', choices: ['dev', 'qa', 'prod'], description: 'Choose deployment environment')
    }

    environment {
        APP_NAME = "demo-app"
        VERSION = "1.0.${BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Cloning the repository....."
                git branch: 'main', url: 'https://github.com/dayakr09-cyber/for-pipeline.git'
            }
        }

        stage('Build') {
            steps {
                echo "Building ${APP_NAME} version ${VERSION}"
                sh 'echo mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo "Running unit tests..."
                sh 'echo mvn test'
            }
        }

        stage('Docker Build') {
            steps {
                echo "Simulating Docker build for ${APP_NAME}:${VERSION}"
                sh 'echo docker build -t ${APP_NAME}:${VERSION} .'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying ${APP_NAME} to ${params.ENV} environment"
            }
        }
    }

    post {
        success {
        }
        failure {
            echo "Pipeline failed "
        }
    }
}
