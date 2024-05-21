pipeline {
    agent any

    environment {
        // Define the port to be used by the application
        APP_PORT = '9999'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Build the Docker image for the application
                    def app = docker.build("sample-app")
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    // Run tests using the built Docker image
                    docker.image("sample-app").inside {
                        sh 'pytest'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Run the application container in detached mode
                    sh 'docker run -d -p ${APP_PORT}:9999 sample-app'
                }
            }
        }
    }
}
