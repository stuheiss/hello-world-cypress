pipeline {
    agent any

/*
    environment {
    }
*/

    options {
        // Keep the 10 most recent builds
        buildDiscarder(logRotator(numToKeepStr:'2'))
    }

    stages {
        stage('Build and Test') {
            steps {
                ansiColor('xterm') {
                    sh "cd e2e; docker-compose up --exit-code-from cypress"
                }
            }
        }
    }

/*
    post {
        always {
            //deleteDir()
        }
    }
*/
}
