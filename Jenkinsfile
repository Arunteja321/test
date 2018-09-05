def buildUserId
def authorizedUserId
pipeline {
    agent any
    stages {
        stage('Populate Build and Authorized Users') {
            steps {
                withCredentials([string(credentialsId: 'authorizedUser', variable: 'user')]) {
                    script {
                        authorizedUserId = user
                    }
                }
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
