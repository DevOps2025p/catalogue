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

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'
                    echo 'Dependencies installed'
                }
            }
        }

        stage('Docker build & push') {
            steps {
                script {
                    withAWS(credentials: 'aws-creds', region: 'ap-south-1') {
                        sh '''
                            aws ecr get-login-password --region ap-south-1 \
                            | docker login --username AWS --password-stdin 802104112912.dkr.ecr.ap-south-1.amazonaws.com

                            docker build -t roboshopcatalogue .
                            docker tag roboshopcatalogue:latest 802104112912.dkr.ecr.ap-south-1.amazonaws.com/roboshopcatalogue:latest
                            docker push 802104112912.dkr.ecr.ap-south-1.amazonaws.com/roboshopcatalogue:latest
                        '''
                    }
                    echo 'Docker build and push complete'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying version ${env.appVersion}...."
            }
        }
    }
}
