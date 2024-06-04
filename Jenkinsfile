pipeline {
    agent any
    environment {
        STAGING_ENVIRONMENT = 'Staging'
        PRODUCTION_ENVIRONMENT = 'Production'
    }
    stages {
        stage('Build') {
            steps {
                echo "Fetching The Source Code"
                echo "Building Code with Maven"
            }
        }
        stage('Unit tests and Integration tests') {
            steps {
                echo "Running Unit Tests with JUnit"
                echo "Running Integration Tests with Selenium"
            }
            post {
                success {
                    echo 'Unit and Integration Tests passed!'
                    emailext(
                        subject: "Pipeline Success: The tests were conducted successfully",
                        body: "The tests; integration and unit, have successfully passed.",
                        from: 'aroomakhan1@outlook.com',
                        to: 's223211992@deakin.edu.au',
                        attachLog: true
                    )
                }
                failure {
                    echo 'Unit and Integration Tests Have Failed!'
                    emailext(
                        subject: "Pipeline Failure: Unit and Integration Tests have failed",
                        body: "The tests; integration and unit, have failed. Please review.",
                        from: 'aroomakhan1@outlook.com',
                        to: 's223211992@deakin.edu.au',
                        attachLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo "Analysing Code with SonarQube"
            }
        }
        stage(' Security Scan') {
            steps {
                echo "Doing Security Scan with OWASP ZAP"
            }
            post {
                success {
                    echo 'Security Scan passed!'
                    emailext(
                        subject: "Pipeline Success: Security Scan has passed successfully",
                        body: "The security scan has successfully passed.",
                        from: 'aroomakhan1@outlook.com',
                        to: 's223211992@deakin.edu.au',
                        attachLog: true
                    )
                }
                failure {
                    echo 'Security Scan failed!'
                    emailext(
                        subject: "Pipeline Failure: Security Scan has failed",
                        body: "The security scan has failed. Please review the security report to find issues.",
                        from: 'aroomakhan1@outlook.com',
                        to: 's223211992@deakin.edu.au',
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploying to Staging') {
            steps {
                echo "Deploying Application to Staging: ${env.STAGING_ENVIRONMENT}"
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo "Running Unit Tests with JUnit"
                echo "Running Integration Tests with Selenium"
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploying to Production Environment: ${env.PRODUCTION_ENVIRONMENT}"
            }
        }
    }
}
