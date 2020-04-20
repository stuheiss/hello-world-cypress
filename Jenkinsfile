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
                sh "docker-compose -d up"
                ansiColor('xterm') {
                    sh "cd e2e; docker run --rm -v `pwd`:/e2e -w /e2e --network hello-world-cypress_default cypress/included:4.4.0 --config baseUrl=http://sentimentalyzer:8123"
                }
                sh "docker-compose down"
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
