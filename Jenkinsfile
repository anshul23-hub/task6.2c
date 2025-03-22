pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'anshul4765.be23@chitkara.edu.in'
        USER_EMAIL = 'anshul4765.be23@chitkara.edu.in'
    }

    tools {
        maven 'Maven'  // Refers to the Maven tool configured in Jenkins
    }

    environment {
        APP_NAME = 'Task6.2C'  // Name of the application
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Cloning the repository from GitHub...'
                checkout scm
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building the application using Maven...'
                // Build using Maven and create a packaged JAR/WAR file
                sh 'mvn clean package -DskipTests'  
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Run tests
                sh 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code quality analysis...'
                // Optional: Add SonarQube or other code analysis here if needed
                // sh 'mvn sonar:sonar -Dsonar.projectKey=Task6.2C'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Optional: Add security scan commands here if needed
                // sh 'mvn dependency-check:check'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                // Add deployment commands if necessary
                sh 'echo "Deploying to Staging..."'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Add integration test commands if required
                sh 'echo "Running integration tests on Staging..."'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                // Add production deployment commands here
                sh 'echo "Deploying to Production..."'
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully! 🎉'
            emailext(
                subject: "${APP_NAME} - Build Successful ✅",
                body: """<p>The build and deployment for <b>${APP_NAME}</b> were successful! 🎉</p>
                        <p><b>Build Details:</b><br>
                        - Application: ${APP_NAME}<br>
                        - Environment: Production<br>
                        - Status: Successful</p>""",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                to: 'anshul4765.be23@chitkara.edu.in',
                mimeType: 'text/html'
            )
        }
        failure {
            echo 'Pipeline failed! ❌ Check the logs for details.'
            emailext(
                subject: "${APP_NAME} - Build Failed ❗",
                body: """<p>The build and deployment for <b>${APP_NAME}</b> failed! ❗</p>
                        <p><b>Build Details:</b><br>
                        - Application: ${APP_NAME}<br>
                        - Environment: Staging/Production<br>
                        - Status: Failed</p>
                        <p>Please check the Jenkins logs for more details.</p>""",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                to: 'anshul4765.be23@chitkara.edu.in',
                mimeType: 'text/html'
            )
        }
    }
}
