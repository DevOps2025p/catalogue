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
                    echo "package version: ${appVersion}"
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                script{
                   sh """
                        npm install
                    """    
                }
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
