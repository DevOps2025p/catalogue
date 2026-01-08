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
                    appVersion = packageJSON.version
                    echo "package version:$(appVersion)"
                
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}