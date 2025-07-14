pipeline {
    agent any

    environment {
        DEPLOY_PATH = "/var/www/html/index.html"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/zubair-tc/JenkinsTask.git'
            }
        }

        stage('Lint HTML') {
            steps {
                script {
                    // Fail pipeline if HTML lint fails
                    sh 'htmlhint basic.html'
                }
            }
        }

        stage('Deploy to Apache') {
            steps {
                script {
                    // Requires sudo permission for Jenkins user (already configured earlier)
                    sh '''
                        echo "Deploying HTML to Apache..."
                        sudo cp basic.html $DEPLOY_PATH
                    '''
                }
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Build failed. Fix linting or deployment issue.'
        }
    }
}
