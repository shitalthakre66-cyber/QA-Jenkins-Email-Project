pipeline {
    agent any

    tools {
        maven 'Maven-3.9.16'
    }

    stages {

        stage('Build and Test') {
            steps {
                bat 'mvn clean test'
            }
        }
    }

    post {

        success {
            emailext(
                subject: "✅ SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                <h2>Test Execution Successful</h2>

                <p><b>Job:</b> ${env.JOB_NAME}</p>
                <p><b>Build:</b> ${env.BUILD_NUMBER}</p>

                <p>All tests executed successfully.</p>

                <p>Build URL:<br>
                ${env.BUILD_URL}</p>
                """,
                mimeType: 'text/html',
                to: 'shitalthakre66@gmail.com'
            )
        }

        failure {
            emailext(
                subject: "❌ FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                <h2>Test Execution Failed</h2>

                <p><b>Job:</b> ${env.JOB_NAME}</p>
                <p><b>Build:</b> ${env.BUILD_NUMBER}</p>

                <p>Please review Jenkins console logs.</p>

                <p>Build URL:<br>
                ${env.BUILD_URL}</p>
                """,
                mimeType: 'text/html',
                to: 'shitalthakre66@gmail.com'
            )
        }

        always {
            archiveArtifacts artifacts: '**/surefire-reports/*'
        }
    }
}