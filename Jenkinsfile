@'
pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Run Python Unit Tests') {
            steps {
                sh 'python3 -m unittest discover -v'
            }
        }
    }

    post {
        always {
            script {
                env.BUILD_STATUS = currentBuild.currentResult

                withCredentials([string(credentialsId: 'webex-bot-token', variable: 'WEBEX_TOKEN')]) {
                    sh '''
                        curl -sS -X POST https://webexapis.com/v1/messages \
                          -H "Authorization: Bearer $WEBEX_TOKEN" \
                          -H "Content-Type: application/json" \
                          --data-raw '{"roomId":"Y2lzY29zcGFyazovL3VybjpURUFNOnVzLXdlc3QtMl9yL1JPT00vMGViMGVhODAtZGJmMi0xMWYxLWFmNzItMjNmMzA5Yjc3Yjky","markdown":"Jenkins build '"$BUILD_STATUS"' for '"$JOB_NAME"' #'"$BUILD_NUMBER"'"}'
                    '''
                }
            }
        }
    }
}
'@ | Set-Content Jenkinsfile