pipeline {
    agent any
    environment {
        EMAIL = 'anshul4765.be23@chitkara.edu.in'  
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application... npm and maven can be used for Building... '
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...For testing, JUnit can be used'
            }
            post {
                success {
                    emailext (
                        subject: "Unit Tests Passed",
                        body: "Unit tests completed successfully!.",
                        to: "${EMAIL}"
                    )
                }
                failure {
                    emailext (
                        subject: "Unit Tests Failed",
                        body: "Unit tests failed. Check Jenkins logs.",
                        to: "${EMAIL}"
                    )
                }
                 always {
            emailext subject: "Build Completed: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                     body: "Check console output at ${env.BUILD_URL} to view the results.",
                     to: 'anshul4765.be23@chitkara.edu.in'
        }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis... ESlint can be used for code analysis'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan... Bandit can be used for security scan'
            }
            post {
                success {
                    emailext (
                        subject: "Security Scan Passed",
                        body: "Security scan completed successfully!!!.",
                        to: "${EMAIL}"
                    )
                }
                failure {
                    emailext (
                        subject: "Security Scan Failed",
                        body: "Security vulnerabilities found. Check Jenkins logs.",
                        to: "${EMAIL}"
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment... AWS, Docker can be used in Deploy'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging... Cypress can be used for integration'
                
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment... Heroku could be used for this deployment'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
