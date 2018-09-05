def buildUserId
def authorizedUserId
pipeline {
     options {
        buildDiscarder(logRotator(numToKeepStr: '2'))
    }
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
