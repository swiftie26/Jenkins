pipeline {
    agent any
    stages {
        stage('Send Test Email') {
            steps {
                script {
                    emailext(
                        subject: "Test Email from Jenkins",
                        body: "This is a test email to verify SMTP settings.",
                        to: "ayesha.rana2604@gmail.com"
                    )
                }
            }
        }
    }
}
