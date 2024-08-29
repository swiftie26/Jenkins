pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Task: Build the code using a build automation tool to compile and package the code."
                echo "Tool: Maven"
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Task: Run unit tests to ensure the code functions as expected and integration tests to ensure the different components work together as expected."
                echo "Tool: JUnit (for unit tests) and JUnit with Spring Test (for integration tests)"
            }
            post {
                always {
                    script {
                        def stageStatus = currentBuild.currentResult
                        def logContent = sh(script: 'cat target/surefire-reports/*.xml', returnStdout: true)
                        emailext body: """${env.STAGE_NAME} stage has completed with status: ${stageStatus}.
                                        Please check the attached logs for details.""",
                                 subject: "${env.STAGE_NAME} Status: ${stageStatus}",
                                 to: "ayesha.rana2604@gmail.com",
                                 attachmentsPattern: '**/target/surefire-reports/*.xml',
                                 mimeType: 'text/plain',
                                 attachLog: true
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Task: Perform static code analysis to ensure the code meets industry standards and best practices."
                echo "Tool: SonarQube"
            }
        }

        stage('Security Scan') {
            steps {
                echo "Task: Perform a security scan on the code to identify any vulnerabilities."
                echo "Tool: OWASP Dependency-Check"
            }
            post {
                always {
                    script {
                        def stageStatus = currentBuild.currentResult
                        def logContent = sh(script: 'cat target/dependency-check-report.html', returnStdout: true)
                        emailext body: """${env.STAGE_NAME} stage has completed with status: ${stageStatus}.
                                        Please check the attached logs for details.""",
                                 subject: "${env.STAGE_NAME} Status: ${stageStatus}",
                                 to: "ayesha.rana2604@gmail.com",
                                 attachmentsPattern: '**/target/dependency-check-report.html',
                                 mimeType: 'text/plain',
                                 attachLog: true
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Task: Deploy the application to a staging server."
                echo "Tool: AWS CodeDeploy"
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Task: Run integration tests on the staging environment to ensure the application functions as expected in a production-like environment."
                echo "Tool: Selenium"
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Task: Deploy the application to a production server."
                echo "Tool: AWS CodeDeploy"
            }
        }
    }

    post {
        always {
            script {
                emailext body: "The pipeline has completed. Please see the attached log for details.",
                         subject: "Pipeline Status: ${currentBuild.currentResult}",
                         to: "ayesha.rana2604@gmail.com",
                         attachLog: true
            }
        }
        success {
            emailext body: "The pipeline completed successfully.",
                     subject: "Pipeline Status: SUCCESS",
                     to: "ayesha.rana2604@gmail.com"
        }
        failure {
            emailext body: "The pipeline failed. Please check the Jenkins logs for more details.",
                     subject: "Pipeline Status: FAILURE",
                     to: "ayesha.rana2604@gmail.com",
                     attachLog: true
        }
    }
}
