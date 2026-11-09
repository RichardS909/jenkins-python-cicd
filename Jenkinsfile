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
            echo "Build result: ${currentBuild.currentResult}"
        }
    }
}
