pipeline {
    agent any
    triggers {
        githubPush()
    }

    environment {
        GITHUB_TOKEN = credentials('github-token')
    }

    stages {
        stage('Run Script') {
            steps {
                script {
                    try {
                        sh 'python3 main.py'
                        currentBuild.result = 'SUCCESS'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
        }
    }
    
    post {
        always {
            script {
                def repoUrl = "https://api.github.com/repos/sparshk380/Jenkins/statuses/${env.GIT_COMMIT}"
                def status = currentBuild.result == 'SUCCESS' ? 'success' : 'failure'
                
                withCredentials([string(credentialsId: 'github-token', variable: 'GITHUB_TOKEN')]) {
                    sh """
                        curl -H "Authorization: token $GITHUB_TOKEN" \
                             -H "Content-Type: application/json" \
                             -d '{
                                 "state": "${status}",
                                 "target_url": "${env.BUILD_URL}",
                                 "description": "Jenkins Build ${status}",
                                 "context": "jenkins-ci"
                             }' \
                             ${repoUrl}
                    """
                }
            }
        }
    }
}
