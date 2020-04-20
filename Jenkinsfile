pipeline {
    agent any

    environment {
        PREFIX = sh(returnStdout: true, script: "echo '${GIT_BRANCH}_${BUILD_NUMBER}_${BUILD_ID}'").trim()
    }

    options {
        // Keep the 10 most recent builds
        buildDiscarder(logRotator(numToKeepStr:'2'))
    }

    stages {
        stage('Build and Test') {
            steps {
                sh "docker-compose -p ${PREFIX} up -d"
                sh "docker network ls"
                ansiColor('xterm') {
                    sh "cd e2e; docker run --rm -v `pwd`:/e2e -w /e2e --network ${PREFIX}_default cypress/included:4.4.0 --config baseUrl=http://sentimentalyzer:8123"
                }
            }
        }
    }

    post {
        always {
            sh "docker-compose -p ${PREFIX} down"
            //deleteDir()
        }
    }
}
