pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'echo Building...'
                // Add your build commands here
            }
        }
        stage('Test') {
            steps {
                sh 'echo Testing...'
                // Add your test commands here
            }
        }
        stage('Run Python Script') {
            steps {
                script {
                    def output = sh(script: 'python3 main.py', returnStdout: true).trim()
                    echo output
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'echo Deploying...'
                // Add your deployment commands here
            }
        }
    }
}
