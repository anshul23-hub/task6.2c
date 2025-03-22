pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'anshul4765.be23@chitkara.edu.in'
        USER_EMAIL = 'anshul4765.be23@chitkara.edu.in'
    }

    stages {
        // Stage 1: Build
        stage('Build') {
            steps {
                echo 'Building the application using Maven...'
                bat 'mvn clean package' // Using Maven on Windows
            }
        }

        // Stage 2: Unit and Integration Tests
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit...'
                bat 'mvn test' // Running tests on Windows
            }
        }

        // Stage 3: Code Analysis
        stage('Code Analysis') {
            steps {
                echo 'Performing static code analysis using SonarQube...'
                bat 'sonar-scanner' // Running SonarQube on Windows
            }
        }

        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP...'
                bat 'zap-cli quick-scan http://your-app-url' // Running OWASP ZAP on Windows
            }
        }

        // Stage 5: Deploy to Staging
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server...'
                bat 'pscp -i private_key.ppk target/*.jar ubuntu@staging-server:/path/to/app' // Using pscp for Windows
            }
        }

        // Stage 6: Integration Tests on Staging
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging using Postman...'
                bat 'newman run staging_tests.json' // Using Newman CLI on Windows
            }
        }

        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server...'
                bat 'pscp -i private_key.ppk target/*.jar ubuntu@prod-server:/path/to/app' // Using pscp for Windows
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
            emailext attachLog: true,
            to: "${USER_EMAIL}",
            subject: "Pipeline Execution Successful",
            body: "The entire pipeline has completed successfully."
        }
        failure {
            echo 'Pipeline failed! Check the logs for more details.'
            emailext attachLog: true,
            to: "${USER_EMAIL}",
            subject: "Pipeline Execution Failed",
            body: "The pipeline has failed. Please check the Jenkins logs for more details."
        }
    }
}
