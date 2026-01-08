pipeline {
    agent {
        label 'jenkinsagent'
    }
    environment {
        appVersion = ''
    }

    stages {
        stage('Read package.json') {
            steps {
                script {
                    def packageJSON = readJSON file: 'package.json'
                    env.appVersion = packageJSON.version
                    echo "package version: ${env.appVersion}"
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying version ${env.appVersion}...."
            }
        }
    }
}
