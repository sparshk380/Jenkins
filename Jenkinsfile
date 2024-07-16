pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Run Python Script') {
            steps {
                script {
                    def output = sh(script: 'python3 main.py', returnStdout: true).trim()
                    echo output
                }
            }
        }
    }
}
