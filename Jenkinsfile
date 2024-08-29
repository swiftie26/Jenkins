pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building the code using Maven"
                // Example build step
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running Unit and Integration Tests"
                // Example test step
            }
            post {
                always {
                    script {
                        def stageStatus = currentBuild.currentResult
                        emailext to: "ayesha.rana2604@gmail.com",
                                 subject: "Unit and Integration Tests Stage: ${stageStatus}",
                                 body: "The Unit and Integration Tests stage has completed with status: ${stageStatus}. The full logs are attached.",
                                 attachLog: true,
                                 mimeType: 'text/html'
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Performing Code Analysis with SonarQube"
                // Example code analysis step
            }
        }

        stage('Security Scan') {
            steps {
                echo "Performing Security Scan with OWASP Dependency-Check"
                // Example security scan step
            }
            post {
                always {
                    script {
                        def stageStatus = currentBuild.currentResult
                        emailext to: "ayesha.rana2604@gmail.com",
                                 subject: "Security Scan Stage: ${stageStatus}",
                                 body: "The Security Scan stage has completed with status: ${stageStatus}. The full logs are attached.",
                                 attachLog: true,
                                 mimeType: 'text/html'
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying to Staging Server"
                // Example deploy step
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running Integration Tests on Staging"
                // Example integration tests on staging step
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying to Production Server"
                // Example deploy step
            }
        }
    }

    post {
        success {
            emailext to: "ayesha.rana2604@gmail.com",
                     subject: "Pipeline Status: SUCCESS",
                     body: "The pipeline completed successfully. The full logs are attached.",
                     attachLog: true,
                     mimeType: 'text/html'
        }

        failure {
            emailext to: "ayesha.rana2604@gmail.com",
                     subject: "Pipeline Status: FAILURE",
                     body: "The pipeline failed. Please check the attached logs for more details.",
                     attachLog: true,
                     mimeType: 'text/html'
        }
    }
}
