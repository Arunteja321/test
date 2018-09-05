def buildUserId
def authorizedUserId
pipeline {
    options {
        buildDiscarder(logRotator(numToKeepStr: '1'))
    }
    agent any
    stages {
        stage('Populate Build and Authorized Users') {
            steps {
                wrap([$class: 'BuildUser']) {
                    script {
                        buildUserId = env.BUILD_USER_ID
                    }
                }
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
