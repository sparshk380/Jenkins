pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub
                git branch: 'main', url: 'https://github.com/sparshk380/Jenkins'
            }
        }

        stage('Display Python File Content') {
            steps {
                script {
                    // List the files in the repository
                    sh 'ls -l'

                    // Display the content of the Python file
                    sh 'cat your_python_file.py'
                }
            }
        }
    }

    post {
        always {
            // Archive artifacts if needed
            archiveArtifacts artifacts: '**/*.py', allowEmptyArchive: true
        }
    }
}
