pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'anshul4765.be23@chitkara.edu.in'
        USER_EMAIL = 'anshul4765.be23@chitkara.edu.in'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'mvn clean package'  // Using Maven for Java builds
            }
            post {
                always {
                    emailext to: "${USER_EMAIL}",
                    subject: "Build Stage Completed",
                    body: "The build stage has completed. Check Jenkins logs for details."
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                sh 'mvn test'  // Running unit and integration tests with Maven
            }
            post {
                always {
                    emailext to: "${USER_EMAIL}",
                    subject: "Unit and Integration Tests Completed",
                    body: "The unit and integration tests have completed. Check Jenkins logs for details."
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing static code analysis...'
                sh 'mvn sonar:sonar'  // Using SonarQube for code analysis
            }
            post {
                always {
                    emailext to: "${USER_EMAIL}",
                    subject: "Code Analysis Completed",
                    body: "The code analysis stage has completed. Check Jenkins logs for details."
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                sh 'snyk test'  // Using Snyk for security vulnerability scanning
            }
            post {
                always {
                    emailext to: "${USER_EMAIL}",
                    subject: "Security Scan Completed",
                    body: "The security scan has completed. Check Jenkins logs for details."
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                sh 'scp target/*.jar user@staging-server:/deploy/'  // Copying build to staging
            }
            post {
                always {
                    emailext to: "${USER_EMAIL}",
                    subject: "Deployment to Staging Completed",
                    body: "Deployment to the staging environment has completed. Check Jenkins logs for details."
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                sh 'curl -X GET http://staging-server/health'  // Checking staging health
            }
            post {
                always {
                    emailext to: "${USER_EMAIL}",
                    subject: "Integration Tests on Staging Completed",
                    body: "Integration tests on staging have completed. Check Jenkins logs for details."
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                sh 'scp target/*.jar user@production-server:/deploy/'  // Copying build to production
            }
            post {
                always {
                    emailext to: "${USER_EMAIL}",
                    subject: "Deployment to Production Completed",
                    body: "Deployment to production has completed. Check Jenkins logs for details."
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
            emailext to: "${USER_EMAIL}",
            subject: "Pipeline Execution Successful",
            body: "The entire pipeline has completed successfully."
        }
        failure {
            echo 'Pipeline failed! Check the logs for more details.'
            emailext to: "${USER_EMAIL}",
            subject: "Pipeline Execution Failed",
            body: "The pipeline has failed. Please check the Jenkins logs for more details."
        }
    }
}
