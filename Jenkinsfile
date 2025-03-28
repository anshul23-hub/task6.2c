pipeline {
    agent any
    environment {
        NOTIFY_EMAIL = 'anshul4765.be23@chitkara.edu.in'
    }

    stages {
        stage('Initialize Build') {
            steps {
                echo 'Initiating the build process... Tools such as npm or Maven can be utilized.'
            }
        }

        stage('Run Unit and Integration Tests') {
            steps {
                echo 'Executing unit and integration tests... JUnit can be employed here.'
            }
            post {
                success {
                    emailext (
                        subject: "Success: Unit Tests Passed",
                        body: "Unit tests executed successfully. No issues found.",
                        to: "${NOTIFY_EMAIL}"
                    )
                }
                failure {
                    emailext (
                        subject: "Error: Unit Tests Failed",
                        body: "Unit tests encountered errors. Review Jenkins logs for details.",
                        to: "${NOTIFY_EMAIL}"
                    )
                }
            }
        }

        stage('Static Code Analysis') {
            steps {
                echo 'Conducting code quality analysis... ESLint is recommended for JavaScript code.'
            }
        }

        stage('Security Check') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    echo 'Performing security checks... Bandit can be used for Python code analysis.'
                }
            }
            post {
                success {
                    emailext (
                        subject: "Success: Security Scan Completed",
                        body: "No vulnerabilities found during the security scan.",
                        to: "${NOTIFY_EMAIL}"
                    )
                }
                failure {
                    emailext (
                        subject: "Warning: Security Scan Failed",
                        body: "Potential security threats detected. Investigate immediately.",
                        to: "${NOTIFY_EMAIL}"
                    )
                }
            }
        }

        stage('Staging Deployment') {
            steps {
                echo 'Deploying to the staging environment... Consider using Docker or AWS.'
            }
        }

        stage('Integration Testing on Staging') {
            steps {
                retry(2) {
                    echo 'Executing integration tests in the staging environment... Cypress can be used.'
                }
            }
        }

        stage('Approval for Production Deployment') {
            steps {
                input message: 'Are you ready to proceed with the production deployment?', ok: 'Proceed'
            }
        }

        stage('Production Deployment') {
            steps {
                echo 'Pushing the build to the production environment... Heroku is a possible choice.'
            }
        }
    }

    post {
        always {
            emailext (
                subject: "Pipeline Status: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "Pipeline execution is complete. Visit ${env.BUILD_URL} to view details.",
                to: "${NOTIFY_EMAIL}"
            )
        }
    }
}
