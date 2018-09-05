def buildUserId
def authorizedUserId
pipeline {
    agent any
    stages {
        stage('Populate Build and Authorized Users') {
            steps {
                echo buildUserId
                echo authorizedUserId
            }
        }
        stage('Deploy to Test') {
            when {
                expression { buildUserId.equals(authorizedUserId) }
            }
            steps {
                echo "Deploying to Test"
            }
        }
    }
}
