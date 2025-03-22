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
                sh 'mvn clean package' // Using Maven as the build automation tool
            }
            post {
                always {
                    emailext attachLog: true,
                    to: "${USER_EMAIL}",
                    subject: "Build Stage Completed",
                    body: "The build stage has completed. Check Jenkins logs for details."
                }
            }
        }

        // Stage 2: Unit and Integration Tests
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit...'
                sh 'mvn test' // Running tests using JUnit
            }
            post {
                always {
                    emailext attachLog: true,
                    to: "${USER_EMAIL}",
                    subject: "Unit and Integration Tests Completed",
                    body: "The unit and integration tests have completed. Check Jenkins logs for details."
                }
            }
        }

        // Stage 3: Code Analysis
        stage('Code Analysis') {
            steps {
                echo 'Performing static code analysis using SonarQube...'
                sh 'sonar-scanner' // Using SonarQube for code analysis
            }
            post {
                always {
                    emailext attachLog: true,
                    to: "${USER_EMAIL}",
                    subject: "Code Analysis Completed",
                    body: "The code analysis stage has completed. Check Jenkins logs for details."
                }
            }
        }

        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP...'
                sh 'zap-cli quick-scan http://your-app-url' // Using OWASP ZAP for security scan
            }
            post {
                always {
                    emailext attachLog: true,
                    to: "${USER_EMAIL}",
                    subject: "Security Scan Completed",
                    body: "The security scan has completed. Check Jenkins logs for details."
                }
            }
        }

        // Stage 5: Deploy to Staging
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server on AWS EC2...'
                sh 'scp target/*.jar ubuntu@staging-server:/path/to/app' // Deploying to AWS EC2
            }
            post {
                always {
                    emailext attachLog: true,
                    to: "${USER_EMAIL}",
                    subject: "Deployment to Staging Completed",
                    body: "Deployment to the staging environment has completed. Check Jenkins logs for details."
                }
            }
        }

        // Stage 6: Integration Tests on Staging
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging using Postman...'
                sh 'newman run staging_tests.json' // Using Postman Newman CLI to run tests
            }
            post {
                always {
                    emailext attachLog: true,
                    to: "${USER_EMAIL}",
                    subject: "Integration Tests on Staging Completed",
                    body: "Integration tests on staging have completed. Check Jenkins logs for details."
                }
            }
        }

        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server on AWS EC2...'
                sh 'scp target/*.jar ubuntu@prod-server:/path/to/app' // Deploying to production server
            }
            post {
                always {
                    emailext attachLog: true,
                    to: "${USER_EMAIL}",
                    subject: "Deployment to Production Completed",
                    body: "Deployment to production has completed. Check Jenkins logs for details."
                }
            }
        }
    }

    // Final Notification for Success or Failure
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
