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
                npx newman run "Contract Testing.postman_collection.json"^
                --reporters cli,htmlextra ^
                --reporter-htmlextra-export "newman-report.html"
                '''
            }
        }
        
    }

    post {
        always {
            echo "Postman test execution completed."
        }
    }
}
