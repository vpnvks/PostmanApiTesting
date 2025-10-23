pipeline {
    agent any

    environment {
        IMAGE_NAME = "vpnvks01/postman-runner:latest"
        COLLECTION_FILE = "Contract_Testing.postman_collection.json"
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone your GitHub repo
                checkout scm
            }
        }

        stage('Run Postman Collection in Docker') {
            steps {
                script {
                    // Convert Windows workspace path for Docker
                    def workspacePath = env.WORKSPACE.replaceAll('\\\\', '/')

                    // Run Docker using Windows batch command
                    bat """
                    docker run --rm -v "${workspacePath}:/workspace" ${IMAGE_NAME} ^
                    npx newman run "/workspace/${COLLECTION_FILE}"
                    """
                }
            }
        }
    }
}
