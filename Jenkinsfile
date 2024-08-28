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
                if (env.STAGE_NAME == 'Unit and Integration Tests' || env.STAGE_NAME == 'Security Scan') {
                    def stageStatus = currentBuild.currentResult
                    mail to: "ayesha.rana2604@gmail.com",
                         subject: "${env.STAGE_NAME} Status: ${stageStatus}",
                         body: "${env.STAGE_NAME} stage has completed with status: ${stageStatus}. Please check the Jenkins logs for details.",
                         attachmentsPattern: '**/target/surefire-reports/*.xml, **/dependency-check-report.html'
                }
            }
        }
        success {
            mail to: "ayesha.rana2604@gmail.com",
                 subject: "Pipeline Status: SUCCESS",
                 body: "The pipeline completed successfully."
        }
        failure {
            mail to: "ayesha.rana2604@gmail.com",
                 subject: "Pipeline Status: FAILURE",
                 body: "The pipeline failed. Please check the Jenkins logs for more details."
        }
    }
}
