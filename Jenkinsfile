pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    environment{
        def appversion = '' //variable declaration
    }
    stages {
        stage('read the version') {
            steps{
                script{
                    def packageJson = readJson file: 'package.json'
                    appversion = packageJson.version
                    echo "application version: $appversion"
                }
            }
        }
        stage('Install Dependencies') {
            steps {
               sh """
                npm install
                ls -ltr
                echo "application version: $appversion"
                """
            }
        }
        stage('Build'){
            steps{
                sh """
                zip -t backend-${appVersion}.zip * -x Jenkinsfile -x backend-${appVersion}.zip
                ls -ltr
                """
            }
        }
    }
    post {
        always {
            echo 'I will always say Hello again!'
            deleteDir()
        }
        success {
            echo 'I will run when pipeline is success'
        }
        failure {
            echo 'I will run when pipeline is failure'
            }
        }
    }



