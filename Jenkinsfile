pipeline {
    agent any

    stages {
        stage('Install Newman') {
            steps {
                bat 'npm install -g newman newman-reporter-htmlextra'
            }
        }

        stage('Run Postman Tests') {
            steps {
                bat '''
                newman run "postman\\MyCollection.postman_collection.json" ^
                --reporters cli,htmlextra ^
                --reporter-htmlextra-export "newman-report.html"
                '''
            }
        }

        stage('Publish Report') {
            steps {
                archiveArtifacts artifacts: 'newman-report.html', fingerprint: true
            }
        }
    }

    post {
        always {
            echo "Postman test execution completed."
        }
    }
}
